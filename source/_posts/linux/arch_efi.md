---
title: Arch Linux 安装:使用gdisk建立EFI分区和Linux分区 For VirtualBox 安装虚拟机
date:  2020/11/22
tags:  [ 'linux', 'Arch', 'Python' ]
---

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)

## 另外一种Arch Linux 安装: 使用gdisk建立EFI分区和Linux分区
	gdisk /dev/sda

- 直接打o，意味着create a new empty GUID partition table (GPT)，回车
- 接下来，打n，新建分区,EFI分区用来储存引导文件,分区代码 EF00 表示efi分区
- 再建立Linux分区，直到Hex code这行，打8300，8300是linux的文件系统。

- 检查,看到文件系统 GPT，2个分区分别是EFI system partition 和 Linux filesystem
```
# gdisk -l /dev/sda

Found valid GPT with protective MBR; using GPT.
Disk /dev/sda: 16777216 sectors, 8.0 GiB
Disk identifier (GUID): B60E27F0-F574-4AAB-B0C1-BAEC5377DDFD
Number  Start (sector)    End (sector)  Size       Code  Name
   1            2048         1050623   512.0 MiB   EF00  EFI system partition  # EFI分区主要放引导文件其实128M够用了
   2         1050624        16777182   7.5 GiB     8300  Linux filesystem
```

### 格式化分区和挂载分区有相应修改，再按上面安装Arch系统
```
mkfs.vfat -F 32  /dev/sda1
mkfs.ext4 /dev/sda2
mount /dev/sda2 /mnt
mkdir -p  /mnt/boot
mount /dev/sda1 /mnt/boot
```

###  中间安装步骤，参考arch 安装命令中文文档
- https://wiki.archlinux.org/index.php/Installation_guide_(简体中文)

## 不装GRUB，使用系统自带的systemd bootctl

```
bootctl install
```

```
# vim /boot/loader/loader.conf

default arch
timeout 1

#console-mode keep
default 75ece990f54f40eba924862b4f752aa6-*
```

```
vim /boot/loader/entries/arch.conf

title   Arch Linux
linux   /vmlinuz-linux
initrd  /initramfs-linux.img
options root=PARTUUID=470b42a8-69bf-4822-ad1a-8164c741b17c rw
```

### 查看磁盘分区UUID号
```
partx /dev/sda
NR   START      END  SECTORS SIZE NAME                 UUID
 1    2048  1050623  1048576 512M EFI system partition 0d180520-7c33-4899-9e8e-30272e072fb4
 2 1050624 16777182 15726559 7.5G Linux filesystem     470b42a8-69bf-4822-ad1a-8164c741b17c

```


