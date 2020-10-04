# Linux

最终目的是增进对Linux系统的理解并提高用命令行解决问题的能力，而不是满足折腾的欲望，沉醉于虚假的成就感中。

### 权限管理

`chmod <权限范围>[+-=]<权限设置> [file]`

权限范围：u(所有者),g(所有组),o(其他人),a(所有人)

权限设置：rwx

### Arch安装

一些文档

[Official Guide on ArchWiki](https://wiki.archlinux.org/index.php/Installation_guide)

[Win10&Arch双系统](https://www.dazhuanlan.com/2019/10/19/5daa648a48222/)

##### 网络

`ip link`查看网卡状态

- ip link set wlan0 up激活设备

`wifi-menu`最方便，20200701未预装

`iwctl`进入iwd提示符

1. `device list`
2. `station *devicename* scan`
3. `station *devicename* get-networks`
4. `station *devicename* connect *ssid*`

##### 硬盘分区

可以提前分好，或者`cfdisk`

`fdisk -l`查看分区状况

`mkfs.ext4 /dev/XXX`

`mount /dev/XXX /mnt`挂载至根目录

`mkdir /mnt/boot`建立boot目录，然后挂载ESP分区至此

安装软件包`pacstrap /mnt base base-devel linux linux-firmware`为方便最好加上nano,iwd,networkmanager

`genfstab -U /mnt >> /mnt/etc/fstab`生成fstab文件

`arch-chroot /mnt`切换至arch系统

### 已知问题

1. VMWare报错

   先检查是否装对应kernel版本的linux-headers

   每次开机后再输`sudo modprobe -a vmw_vmci vmmon`

   上述命令亦无效则是kernel版本太新尚无module可用，参见[此贴](https://communities.vmware.com/thread/638824)中的步骤，下载[该仓库](https://github.com/mkubecek/vmware-host-modules)中对应版本执行`make`即可编译完成

   vmnet8报错无法联网：`sudo systemctl start vmware-networks.service`

2. 挂载NTFS分区

   sudo mount -t ntfs-3g /dev/*nvme0n1p4* /home/*username*/*XXX*

   该命令仅限一次开机，永久生效需编辑/etc/fstab

