



---

## minicom

minicom linux下好用的串口通讯工具:

```
$ minicom -D /dev/ttyUSB0
```

## tree 

打印树型目录结构，可指定层数。

```
$ tree -L 3
```

## locate

 利用文件索引缓存快速全盘查找文件

## progress（cv）

<https://github.com/Xfennec/progress>

 coreutils viewer，显示coreutils 中的基本命令的进度，比如 cp、mv、rm、dd、tar，基本用法`progress -wm`

安装：

```bash
$ yay -S progress-git
```

别名`cv`放~/.bashrc里：
```
#progress
alias cv="progress -w"
```



## lm_sensors

查看传感器温度，cpu、主板、显卡温度等。

```
[r@r-pc test-activity]$ sensors 
k10temp-pci-00c3
Adapter: PCI adapter
Tdie:         +43.2°C  (high = +70.0°C)
Tctl:         +43.2°C  

amdgpu-pci-3800
Adapter: PCI adapter
vddgfx:           N/A  
vddnb:            N/A  
fan1:             N/A
temp1:        +43.0°C  (crit = +80.0°C, hyst =  +0.0°C)


```



## Time Cat （tcat）

https://github.com/marcomorain/tcat

给每一行文本打上时间戳



## Pacapt

安装方法：https://github.com/icy/pacapt#installation

包管理器的命令行包装，用于把大多数包管理器的命令转成arch系的pacman式命令，用法：

```
$ pacapt -Ss somepackage
```


## mplayer

在framebuffer全屏循环播放视频：

```
$ mplayer -fs -loop 0 -vo fbdev xxx.mp4
```


## homebrew

macos自带的包管理器，其实Linux和windows的WSL也能用。

可以在home目录下安装软件，不需要root权限。

## screenfetch Linux系统摘要打印

一键打印当前linux的信息摘要

## ncdu unix命令行下磁盘空间占用统计

`Disk usage analyzer with an ncurses interface`

![20201222153024](_assets/linux常用工具/20201222153024.png)

## X11下复制文本到粘贴板

Linux桌面，常需要手动复制命令行下当前路径

1. 实际复制的操作可以用命令完成，需要安装`xsel`和`xclip`工具：

```
$ echo barhaha123 | xclip -selection c
```

2. 简化操作

```
$ alias xclip='xclip -selection c'
$ pwd |xcilp
```

