# 阿里云ECS七天实践营

## [Day1 VuePress打造专属云笔记](https://edu.aliyun.com/course/399)

[VuePress中文官网](https://www.vuepress.cn)

### **前置步骤**  

- 记得设置ECS安全组(22,8080端口，授权对象0.0.0.0/0)  
- 安装Node.js
  1. 下载安装包`wget https://npm.taobao.org/mirrors/node/v13.9.0/node-v13.9.0-linux-x64.tar.xz`
  2. 创建安装⽬录`sudo mkdir -p /usr/local/lib/nodejs`
  3. 解压文件到安装⽬录`sudo tar -xJvf node-v13.9.0-linux-x64.tar.xz -C /usr/local/lib/nodejs`
  4. 使⽤查看node.js版本号命令验证  
     进入目录`cd /usr/local/lib/nodejs/node-v13.9.0-linux-x64/bin` 
     执行`./node -v`
  5. 修改环境变量  
     `nano ~/.bash_profile`,找到`PATH=$PATH:$HOME/bin`,在其后添加`:/usr/local/lib/nodejs/node-v13.9.0-linux-x64/bin`,保存后再重载`source ~/.bash_profile`

### **安装VuePress**

1. 下载安装  
   `npm config set registry https://registry.npm.taobao.org`  
   `npm install -g vuepress`
2. 创建文件夹作为目录并进入  
   `mkdir try_blogs`    `cd try_blogs`
3. 项目初始化  
   `npm init -y `完成后生成`package.json`文件

### 配置VuePress

1. 修改`package.json`  
   将scripts中内容改为如下  
   `"scripts": {
   "docs:dev": "vuepress dev docs",
   "docs:build": "vuepress build docs"
   }`
   
2. 在当前目录中创建文档目录  
   `mkdir docs`
   
3. 在`docs`目录下创建.vuepress目录  
   `cd docs`
   `mkdir .vuepress`
   
4. 新建README文件(`docs`目录下)  
   `echo '# Hello VuePress - first blog!' >README.md`
   
5. 在`.vuepress`目录下创建`config.js`文件  
   `cd .vuepress`
   `echo >config.js`
   
6. 创建`public`目录(`.vuepress`目录下)  
   `mkdir public`
   
7. 完成后的工作目录如下:
   try_blogs  
   ├─ docs //在这里面写文章,直接在此文件夹下新建文件夹,然后再建md文档,链接会自动生成  
   │ ├─ README.md // 这个将会是我们以后的首页  
   │ └─ .vuepress // 这个里面会存放一些配置和组件  
   │ └─ public // 静态文件存放地  
   │ └─ config.js //配置文件,以后的所有配置基本都在这里写  
   └─ package.json
   
8. 回到`try_blogs`目录，执行`vuepress dev docs`运行本地服务，访问8080端口即可预览

   ---

## [Day2 搭建MediaWiki知识库](https://edu.aliyun.com/course/425)

### 安装运行环境

- LAMP:镜像市场自带

### 安装MediaWiki

工具:PuTTY,FileZiila

1. 下载MediaWiki并解压缩`https://releases.wikimedia.org/mediawiki/1.29/mediawiki-1.29.1.tar.gz`
2. 在`/data/wwwroot/default/`目录下创建`old`文件夹，将原来文件全部移至`old`目录
3. 把解压后的MediaWiki文件上传至`/data/wwwroot/default/`目录
   `chown -R www /data/wwwroot/default`为目录赋权
4. 访问公网IP即可开始初始设置
5. 最后下载LocalSettings.php配置文件上传到该目录

### 使用MediaWiki

登录管理员帐号后即可自行操作

---

## [Day3 基于ECS构建微信公众号管理系统](https://edu.aliyun.com/course/428)

### 前置步骤

- LAMP环境
- SSH客户端(PuTTY),FTP客户端(FileZilla)

### 安装微擎

1. 进入`/data/wwwroot/default/`目录，将原有文件移至新建`old`文件夹，将微擎安装文件上传至该目录

2. 为目录赋权`chown -R www /data/wwwroot/default`
   `chown -R www /data/wwwroot/default/data`

3. 数据库密码`grep dbrootpwd /root/oneinstack/options.conf`
   会提示`dbrootpwd='KeYpZrZx'`，即默认root密码KeYpZrZx
4. 打开`http://公网IP/old/phpmyadmin`，输入`root`账户密码登录
5. 在左侧列表点击【new】创建新数据库，可命名为newdb
6. 访问`http://公网IP`，点击【install.php 进入安装 >>】
7. ![填写数据库选项](https://edu.aliyun.com/files/course/2019/07-30/16210620e56e010343.png)

8. 回到首页即可用管理员账号登录

### 使用微擎

登录后需要在[http://s.we7.cc/index.php?c=home&a=auth&do=register](http://s.we7.cc/index.php?c=home&a=auth&do=register)注册微擎的云平台账号，然后在后台登录

选择“手动添加微信公众号”后即可管理微信公众号

## Day4 部署离线下载服务器

前置步骤同上

### 安装部署CCAA

CCAA是服务器离线下载解决⽅案包，组件包含了Aria2提供离线下载，AriaNg为Aria2 提供WEB界⾯以及Filemanager提供⽂件管理，ccaa_web⽀撑AriaNg运⾏。

使用一键安装脚本`bash <(curl -Lsk https://raw.githubusercontent.com/helloxz/ccaa/master/ccaa.sh) cdn`，按提示操作设置下载路径和Aria2的RPC密钥。完成后打开`http://公网IP:6080`，点击左侧AriaNG设置，修改Aria2 RPC 密钥为安装时所设值即可。

### CCAA常⽤命令

- ccaa:进⼊CCAA操作界⾯
- ccaa status:查看CCAA运⾏状态 
- ccaa stop:停⽌CCAA 
- ccaa start:启动CCAA 
- ccaa restart:重启CCAA 
- ccaa -v:查看CCAA版本（2.0开始⽀持）

### 使用离线下载服务器

GUI，直接操作即可

## Day5 搭建Java Web开发环境

### 安装JDK

1. 查看yum源中JDK版本`yum list java*`
2. 使用yum安装JDK1.8`yum -y install java-1.8.0-openjdk*`

### 安装MySQL数据库

1. 安装MySQL

   `wget http://dev.mysql.com/get/mysql57-community-release-el7-10.noarch.rpm `

   `yum -y install mysql57-community-release-el7-10.noarch.rpm `

   `yum -y install mysql-community-server`

2. 启动MySQL数据库`systemctl start mysqld.service`

3. 查看MySQL初始密码`grep "password" /var/log/mysqld.log`

4. 登录数据库`mysql -uroot -p`，要求输入初始密码

5. 修改MySQL默认密码  
   `set global validate_password_policy=0;  #修改密码安全策略为低（只校验密码长度，至少8位）。`
   ``ALTER USER 'root'@'localhost' IDENTIFIED BY '12345678';`

6. 授予root用户远程管理权限`GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY '12345678';`

7. 输入`exit`退出MySQL

### 安装Tomcat

1. 下载Tomcat压缩包`wget https://mirror.bit.edu.cn/apache/tomcat/tomcat-8/v8.5.57/bin/apache-tomcat-8.5.57.tar.gz`,然后解压
2. 修改Tomcat名字`mv apache-tomcat-8.5.57 /usr/local/Tomcat8.5`
3. 为Tomcat赋权可运行`chmod +x /usr/local/Tomcat8.5/bin/*.sh`
4. 修改Tomcat默认端口号从8080变为80`sed -i 's/Connector port="8080"/Connector port="80"/' /usr/local/Tomcat8.5/conf/server.xml`
5. 启动Tomcat`/usr/local/Tomcat8.5/bin/./startup.sh`
6. 访问Tomcat，在浏览器打开ECS公网IP即可(默认端口号已修改为80)

