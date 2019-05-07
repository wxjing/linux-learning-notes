# 设置环境变量
## 方法一
***在/etc/profile 中加入：***
```sh
export PATH=$PATH:/usr/local/nginx/sbin
```
***保存，执行 source /etc/profile ，使配置文件生效。***
## 方法二
***命令行***
`export PATH=$PATH:/usr/local/mysql/bin`
`export PATH=$PATH:/Applications/MAMP/bin/php/php7.0.15/bin`


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
