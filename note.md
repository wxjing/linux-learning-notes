[toc]
## Linux常用命令
### 系统安全
sudo su chmod setfacl
### 进程管理
w top ps kill pkill pstree killall
### 用户管理
id usermod useradd groupadd userdel
### 文件系统
mount umount fsck df du
### 系统关机和重启
shutdown reboot
### 网络应用
curl telnet mail elinks
### 网络测试
ping netstat host
### 网络配置
hostname ifconfig
### 常用工具
ssh screen clear who date
### 软件包管理
yum rpm apt-get
### 文件查找和比较
locate find
### 文件内容查看
head tail less more
### 文件处理
touch unlink rename ln cat
### 目录操作
cd mv rm pwd tree cp ls
### 文件权限属性
setfacl chmod chown chgrp
### 压缩、解压
bzip2/bunzip2 gzip/gunzip zip/unzip tar
### 文件传输
ftp scp

## Linux系统定时任务

### crontab命令
`crontab -e`
### at命令
```
# at 2:00 tomorrow
at>/home/Jason/do_job
at>Ctrl+D
```

## shell基础

### 脚本执行方式
赋予权限，直接执行、例如：`chmod +x test.sh;./test.sh`
调用解释器使得脚本执行，例如：bash csh ash bash ksh等
使用source命令，例如：`source test.sh`

## 编写基础
开头用#!指定脚本解析器，例如：`#!/bin/sh`

# 设置环境变量

## 方法一 `/etc/profile`
```sh
export PATH=$PATH:/usr/local/nginx/sbin
```
>保存，执行 source /etc/profile ，使配置文件生效。
## 方法二 命令行

`export PATH=$PATH:/usr/local/mysql/bin`
`export PATH=$PATH:/Applications/MAMP/bin/php/php7.0.15/bin`

## 环境变量文件
- /etc/profile
- /etc/profile.d/*.sh
- ~/.bash_profile
- ~/.bashrc
- /etc/bashrc

## 环境变量文件加载顺序
![加载顺序](./images/WechatIMG498.jpeg)



# 查看网络连接
`netstat -an`
# 查看进程之间的关系
`pstree -p 22727`

# 检测进程是否启动
```php
/*
wc -l :显示多少行
*/
$shell  =  "netstat -anp 2>/dev/null | grep 8811 | grep LISTEN | wc -l";
$result = shell_exec($shell);//返回 0 未启动 1 启动
```

# 平滑重启
```sh
# pid=`pidof live_master`   live_master:进程id
# kill -USR1 $pid   平滑重启
echo "loading..."
pid=`pidof live_master`
echo $pid
kill -USR1 $pid
echo "loading success"
```

# 建立软连接
```sh
ln -s /usr/local/bin/
```

# 安装SSH服务
- 安装SSH
`yum install openssh-server`
- 启动SSH
`service sshd start`
- 设置开机运行
`chkconfig sshd on`

# 认证：
## 本地服务器<--------------->远程服务器

1. 在本地设备中执行下述命令，一路回车即可：
 `ssh-keygen`

2. 密钥对生成之后，可使用scp(安全复制)命令复制公钥：
 `scp ~/.ssh/id_rsa.pub deploy@60.205.178.92:`
> 注意一定要在末尾加上：符号！这个命令会把公钥复制到远程服务器中deploy用户的家目录里。
3. 接下来，一 deploy 用户的身份登录远程服务器。确认 ~/.ssh是否存在，如果不存在则创建：
`mkdir ~/.ssh`
4. 然后执行下述命令：
`touch ~/.ssh/authorized_keys`
5. 这个文件的内容是一系列允许登录这台远程服务器的公钥。执行下述命令复制公钥至该文件：
`cat ~/id_rsa.pub >> ~/.ssh/authorized_keys`

# linux进程后台运行的几种方法
`hangup信号:父进程退出，则会发送hangup信号给所有子进程，子进程收到hangup以后也会退出`
1. 命令后加& 使用`%1`后台进程放入前台 父进程会发送hangup信号
2. `nohup php demo.php >> log.out 2>&1 &` nohup忽略hangup信号
