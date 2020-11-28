---
title: Linux快速入门示例 Vutrl管理和挂载块存储
date:  2020-11-28
tags:  [linux]
---

蘭雅sRGB 个人博客 | [https://262235.xyz](https://262235.xyz)

## 管理和挂载块存储，挂载第二块硬盘也差不多

### Create new empty partitions:  #创建新的空分区
```
parted -s /dev/vdb mklabel gpt
parted -s /dev/vdb unit mib mkpart primary 0% 100%
```

### Create new empty filesystem:  #创建新的空文件系统
```
mkfs.ext4 /dev/vdb1
```

### Mount block storage:  # 挂载块存储
```
mkdir /mnt/blockstorage
echo >> /etc/fstab
echo /dev/vdb1               /mnt/blockstorage       ext4    defaults,noatime,nofail 0 0 >> /etc/fstab
mount /mnt/blockstorage
```

### 建立目录软连接
```
ln -s /mnt/blockstorage  www
```

----
### 附加，使用UUID自动挂载数据盘
```
#  fstab 使用UUID自动挂载数据盘
cat /etc/fstab  #查看当前系统已经存在的挂载信息
# <file system> <mount point>   <type>  <options>       <dump>  <pass>
UUID=8a2aa399-0f5a-4cc1-bc77-5cb008f9a754 /               ext4    errors=remount-ro 0       1
UUID=231a3535-73c5-4245-8e3e-bf546f034d98 /mnt/emby/      ext4    defaults          0       2

blkid  ### 查看磁盘分区的 UUID
blkid /dev/sdb5
/dev/sdb5: UUID="231a3535-73c5-4245-8e3e-bf546f034d98" TYPE="ext4" PARTUUID="aeb779b9-05"
```
