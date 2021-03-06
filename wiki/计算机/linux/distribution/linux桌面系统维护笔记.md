

---



## 救援模式

linux无法启动时，可以进LiveCD，mount整个rootfs，然后chroot，再进行修复操作，如：

```
$ su -
# mkdir rootfs
# mount /dev/sdb2 rootfs
# mount /dev/sdb1 rootfs/boot/efi
# mv /dev ./rootfs/
# mv /proc ./rootfs/
# cd rootfs
# chroot .
```

在archlinux下，使用arch-chroot替代chroot，无需移动设备文件，如：

```
$ sudo pacman-mirrors -c China
$ sudo pacman -Sy
$ sudo pacman -S arch-install-scripts
$ su -
# mkdir rootfs
# mount /dev/sdb2 rootfs
# mount /dev/sdb1 rootfs/boot/efi
# cd rootfs
# arch-chroot .
```



## 重建grub配置

```
# grub-mkconfig -o /boot/efi/grub/grub.cfg
```



## 管理内核

使用指定内核的最简单的方法，`/boot`中用不到的内核镜象全删了，重建grub配置即可。



## 更换显示管理器(Display Managers)

> ref: https://wiki.manjaro.org/index.php/Install_Display_Managers

manjaro默认用lightdm，如要替换成ssdm：

```
$ pamac install sddm
$ sudo systemctl enable sddm.service --force
```

其实更换DM就是修改systemd软链接：

```
$ sudo systemctl enable sddm.service --force
Removed /etc/systemd/system/display-manager.service.
Created symlink /etc/systemd/system/display-manager.service → /usr/lib/systemd/system/sddm.service.
```



## 无法进入桌面的处理方法

图形界面启动流程：

1. 启动x11，x11尝试加载显卡驱动
2. 显示管理器（display manager，如lightdm）启动，它尝试连接X进行显示，它是一个用户登入界面
3. 显示管理器加载窗口管理器session（如i3-session、gnome-session）

使用快捷键Ctrl+Alt+FnX可以切换文字终端，以便排查问题。

### 排查X11问题

尝试在文字终端里启动x11：

```
# startx
```

### 排查显示管理器问题

查看lightdm日志：

```
# systemctl status lightdm.service
```

debug模式启动lightdm：

```
# lightdm --test-mode --debug
```

### 检查显示驱动

显示驱动详细列表：

```
# mhwd -l -d
```

移除/安装：

```
# mhwd -r pci video-linux
# mhwd -i pci video-linux
```

