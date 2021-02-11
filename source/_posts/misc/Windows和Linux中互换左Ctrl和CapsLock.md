---
title: Windows和Linux互换左Ctrl和CapsLock
date: 2021-02-10 19:26:14
tags: windows
categories:
  - misc
---

# Windows和Linux中互换左Ctrl和CapsLock

## Windows

在Win7之后的系统可以通过修改注册表实现，下面是导出的注册表脚本，双击导入即可：

*CapsLockLeftCtrl_switch.reg*

```ini
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Keyboard Layout]

"Scancode Map"=hex:00,00,00,00,00,00,00,00,03,00,00,00,1d,00,3a,00,3a,00,1d,00,00,00,00,00
```

恢复:

*CapsLockLeftCtrl_reset.reg*

```ini
Windows Registry Editor Version 5.00

[HKEY_LOCAL_MACHINE\SYSTEM\ControlSet001\Control\Keyboard Layout]

"Scancode Map"=-
```

### 对于值的解释

1. header version，总为0
2. header flag，总为0
3. 要更改的键条目数和多余的空终止符行的总和。在这种情况下，更改了2个关键项，因此，更改了3个。
4. 当处理CAPS LOCK的代码（0x003a）时发送LEFT CTRL的代码（0x001d）。
5. 步骤4反过来
6. 空行结束

## Linux

一次性更换可使用以下命令：

```shell
setxkbmap -option ctrl:swapcaps
```

如果要实现每次开机都自动实现左Ctrl和CapsLock互换，可以添加以下内容到`~/.Xmodmap`：

```shell
remove Lock = Caps_Lock
keysym Caps_Lock = Control_L
add Control = Control_L
```

然后在`~/.xinitrc`中（不同的系统可能会不一样）添加`xmodmap ~/.Xmodmap`即可。