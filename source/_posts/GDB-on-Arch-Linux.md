---
title: GDB on Arch Linux
date: 2023-11-13 13:25:44
tags: pwn
---

## 在Arch Linux上配置pwndbg + pwngdb
由於不久前剛換Arch Linux，但是發現這上面gdb似乎沒辦法像Ubuntu那樣方便使用

- [pwndbg](https://github.com/pwndbg/pwndbg)
- [pwngdb](https://github.com/scwuaptx/Pwngdb)

先到這兩個地方clone下來 然後運行pwndbg的setup.sh

### gdbinit
接著就會發現heap的指令基本都不能用，所以要修改一下gdbinit

```
set debuginfod enabled on

define peda
	source /usr/share/peda/peda.py
end
define gef
	source /usr/share/gef/gef.py
end

source ~/Apps/pwndbg/gdbinit.py
source ~/Pwngdb/pwngdb.py
source ~/Pwngdb/angelheap/gdbinit.py
define hook-run
python
import angelheap
angelheap.init_angelheap()
end
end
```

### bashrc
最後再設定debug info的載點就好了
```
export DEBUGINFOD_URLS="https://debuginfod.archlinux.org"
```

然後每次debug檔案時她都會自動下載對應的symbols

![img](1.png)
