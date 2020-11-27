# MISC

## 工具

`fcrackzip`

- `-b` 暴力破解
- `-c1`限制密码为数字
- `-l x-y`限制密码长度为x-y之间
  - 直接`-l数字`

文件类型

- linux下`file`命令
- 查看十六进制文件头(WinHex,文本编辑器插件等)
- 记住常见类型文件头

文件分离

- linux下`binwalk`分析,`binwalk -e`分离

- linux下`foremost 文件名 -o 输出目录名`自动分离文件

- linux下`dd`命令手动分离
  `dd if=源文件 of=输出文件 bs=1 skip=开始分离的字节数 count=`
  `#bs 设置读写块的bytes大小`
- win下WinHex手动保存

文件合并

- linux下`cat`命令
  `cat file1 file2 file3 > file`
  `cat file_* >file`
- win下`copy`命令
  `copy file1+file2+file3 file`

文件内容隐写

隐写图片查看器`stegsolve`将两个图片的信息进行XOR,AND,OR操作，或分析数据

`zsteg`工具自动分析

TweakPNG修改PNG图像的元信息存储，当文件头正常却无法打开，用其打开会弹出CRC校验错误的提示，有时CRC没错但高度和宽度不正确需要手动修改

Win下SilentEye工具自动解密图片

linux下StegDetect

查看图片通道、取反、扫二维码

压缩包

伪加密

ARCHPR爆破(字典、明文攻击)

## 刷题

PDF用Word打开，移走图片

gif有帧二维码，缺失定位点自己补全

jar解开看源码，字符串末尾有`=`，尝试base64解码才是flag

纯黑白图片对应二进制10，python判断颜色生成01串，再转文本

linux下`strings`命令输出所有字符串（IDA快捷键Shift+F12同效果)

base64转图片，html可显示

png图片的长宽：从0x0000:0010开始的两个4字节

png图片开头：`89 50 4E 47 0D 0A 1A 0A`

JPG 文件： `FF D8` 开头，`FF D9`结尾

RAR伪加密：尝试打开会报错，第16个字节尾 4改0