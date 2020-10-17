# Linux

最终目的是增进对Linux系统的理解并提高用命令行解决问题的能力，而不是满足折腾的欲望，沉醉于虚假的成就感中。

### 目录结构

- `/bin`、`/sbin`：链接到 `/usr/bin`，存放 Linux 一些核心的二进制文件，其包含的命令可在 shell 上运行。
- `/boot`：操作系统启动时要用到的程序。
- `/dev`：包含了所有 Linux 系统中使用的外部设备。需要注意的是这里并不是存放外部设备的驱动程序，而是一个访问这些设备的端口。
- `/etc`：存放系统管理时要用到的各种配置文件和子目录。
- `/etc/rc.d`：存放 Linux 启动和关闭时要用到的脚本。
- `/lib`、`/lib64`：链接到 `/usr/lib`，存放系统及软件需要的动态链接共享库。
- `/mnt`：这个目录让用户可以临时挂载其他的文件系统。
- `/proc`：虚拟的目录，是系统内存的映射。可直接访问这个目录来获取系统信息。
- `/root`：系统管理员的主目录。
- `/srv`：存放一些服务启动之后需要提取的数据。
- `/sys`：该目录下安装了一个文件系统 sysfs。该文件系统是内核设备树的一个直观反映。当一个内核对象被创建时，对应的文件和目录也在内核对象子系统中被创建。
- `/tmp`：公用的临时文件存放目录。
- `/usr`：应用程序和文件几乎都在这个目录下。
- `/usr/src`：内核源代码的存放目录。
- `/var`：存放了很多服务的日志信息。

### Bash使用

#### 输入输出

- 使用命令的输出作为可执行文件的输入参数
  - `$ ./vulnerable `your_command_here``
  - `$ ./vulnerable $(your_command_here)`
- 使用命令作为输入
  - `$ your_command_here | ./vulnerable`
- 将命令行输出写入文件
  - `$ your_command_here > filename`
- 使用文件作为输入
  - `$ ./vulnerable < filename`

```bash
$var, ${var}      取变量的值
`cmd`, $(cmd)     代换标准输出
# 注意区分$的格式,花括号(或无括号)取变量,圆括号取命令输出
```

#### [Bash快捷键](https://ss64.com/bash/syntax-keyboard.html)

**Moving** 

```
Ctrl + a   Go to the beginning of the line (Home)
Ctrl + e   Go to the End of the line (End)
Ctrl + p   Previous command (Up arrow)
Ctrl + n   Next command (Down arrow)
Alt + b   Back (left) one word
Alt + f   Forward (right) one word
Ctrl + f   Forward one character
Ctrl + b   Backward one character
Ctrl + xx  Toggle between the start of line and current cursor position
```

**Process control:**

```
Ctrl + C   Interrupt/Kill whatever you are running (SIGINT).
Ctrl + s   Stop output to the screen (for long running verbose commands).
Then use PgUp/PgDn for navigation.
Ctrl + q   Allow output to the screen (if previously stopped using command above).
Ctrl + D   Send an EOF marker, unless disabled by an option, this will close the current shell (EXIT).
Ctrl + Z   Send the signal SIGTSTP to the current task, which suspends it.
To return to it later enter fg 'process name' (foreground).
```

#### man查看命令

`man -f command`获得更多命令相关信息

```bash
[dmtsai@study ~]$ man -f man
man (1)
 - an interface to the on-line reference manuals
man (1p )
 - display system documentation
man (7)
 - macros to format man pages
```



### 环境变量

环境变量字符串都是 `name=value` 这样的形式。大多数 name 由大写字母加下画线组成，一般把 name 部分叫做环境变量名，value 部分则是环境变量的值，而且 value 需要以 "/0" 结尾，环境变量定义了该进程的运行环境。

#### 分类

- 按照生命周期划分
  - 永久环境变量：修改相关配置文件，永久生效。
  - 临时环境变量：使用 `export` 命令，在当前终端下生效，关闭终端后失效。
- 按照作用域划分
  - 系统环境变量：对该系统中所有用户生效。
  - 用户环境变量：对特定用户生效。

#### 设置方法

- 在文件 `/etc/profile` 中添加变量，这种方法对所有用户永久生效。如：

  ```
  # Set our default path
  PATH="/usr/local/sbin:/usr/local/bin:/usr/bin"
  export PATH
  ```

  添加后执行命令 `source /etc/profile` 使其生效。

- 在文件 `~/.bash_profile` 中添加变量，这种方法对当前用户永久生效。其余同上。

- 直接运行命令 `export` 定义变量，这种方法只对当前终端临时生效。

### 进程管理

- `top`
  - 可以实时动态地查看系统的整体运行情况。

- `ps`
  - 用于报告当前系统的进程状态。可以搭配 kill 指令随时中断、删除不必要的程序。
  - 查看某进程的状态：`$ ps -aux | grep [file]`，其中返回内容最左边的数字为进程号（PID）。

- `kill`
  - 用来删除执行中的程序或工作。
  - 删除进程某 PID 指定的进程：`$ kill [PID]`

### 用户和组

**UID**(User ID)是对一个用户的单一身份标识，而**GID**(Group ID)则对应多个UID。可以使用 `id` 命令来查看

UID为0的root用户类似于系统管理员，它具有系统的完全访问权

GID 的关系存储在 `/etc/group` 文件中

所有用户的信息（除了密码）都保存在 `/etc/passwd` 文件中，而为了安全起见，加密过的用户密码保存在 `/etc/shadow` 文件中，此文件只有 root 权限可以访问。

### 权限管理

`chmod <权限范围>[+-=]<权限设置> [file]` 

权限范围：u(所有者),g(所属组),o(其他人),a(所有人)

+赋予、-取消、=指定

权限设置

- `r`：读取权限，数字代号为 “4”
- `w`：写入权限，数字代号为 “2”
- `x`：执行或切换权限，数字代号为 “1”

### 文件描述符

### 核心转储

### 调用约定

### procfs

procfs 文件系统是 Linux 内核提供的虚拟文件系统，为访问系统内核数据的操作提供接口。说是虚拟文件系统，是因为它不占用存储空间，而只是占用了内存。用户可以通过 procfs 查看有关系统硬件及当前正在运行进程的信息，甚至可以通过修改其中的某些内容来改变内核的运行状态。

#### /proc/cmdline

在启动时传递给内核的相关参数信息，通常由 lilo 或 grub 等启动管理工具提供

#### /proc/cpuinfo

记录 CPU 相关的信息

#### /proc/crypto

已安装的内核所使用的密码算法及算法的详细信息

#### /proc/devices

已加载的所有块设备和字符设备的信息，包含主设备号和设备组(与主设备号对应的设备类型)名

#### /proc/interrupts

X86/X86_64 系统上每个 IRQ 相关的中断号列表，多路处理器平台上每个 CPU 对于每个 I/O 设备均有自己的中断号

#### /proc/kcore

系统使用的物理内存，以 ELF 核心文件（core file）格式存储

#### /proc/meminfo

系统中关于当前内存的利用状况等的信息

#### /proc/mounts

每个进程自身挂载名称空间中的所有挂载点列表文件的符号链接

#### /proc/modules

当前装入内核的所有模块名称列表，可以由 lsmod 命令使用

#### /proc/slabinfo

保存着监视系统中所有活动的 slab 缓存的信息

#### /proc/[pid]

在 /proc 文件系统下，还有一些以数字命名的目录，这些数字是进程的 PID 号，而这些目录是进程目录。

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

### 中文环境

#### fcitx5

删除词语：^7

`ctrl + alt + shift + u` 查看字符的unicode编码

- 如果你需要查看文本编辑器中选中文字的 Unicode 编码，那么直接选中文字，然后使用快捷键 `ctrl + alt + shift + u` 可以查看选中文字的编码

- 如果你需要查看非编辑区域（比如本 wiki）中文字的 Unicode 编码，那么需要首先将该段文字复制到剪贴板，然后点击任意一个可编辑区域（比如搜索框），然后使用快捷键 `ctrl + alt + shift + u` 可以查看剪贴板中文字的编码

### 已知问题

1. VMWare报错

   先检查是否装对应kernel版本的linux-headers

   每次开机后再输`sudo modprobe -a vmw_vmci vmmon`

   上述命令亦无效则是kernel版本太新尚无module可用，参见[此贴](https://communities.vmware.com/thread/638824)中的步骤，下载[该仓库](https://github.com/mkubecek/vmware-host-modules)中对应版本执行`make`即可编译完成

   vmnet8报错无法联网：`sudo systemctl start vmware-networks.service`

2. 挂载NTFS分区

   sudo mount -t ntfs-3g /dev/*nvme0n1p4* /home/*username*/*XXX*

   该命令仅限一次开机，永久生效需编辑/etc/fstab

