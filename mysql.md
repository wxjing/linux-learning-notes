[TOC]
# 二进制安转
> 1. cd /usr/local/src
> 2. 下载
> - 64位
    - wget http://mirrors.sohu.com/mysql/MySQL-5.5/mysql-5.5.55-linux2.6-x86_64.tar.gz
> - 32位
    - wget http://mirrors.sohu.com/mysql/MySQL-5.5/mysql-5.5.55-linux2.6-i686.tar.gz
> 3. tar zxf mysql-5.5.45-linux2.6-x86_64.tar.gz
> 4. mv mysql-5.5.45-linux2.6-x86_64 /usr/local/mysql
> 5. cd /usr/local/mysql

1. groupadd mysql
2. useradd -r -g mysql mysql
4. chown -R mysql .
5. chgrp -R mysql .
6. ./scripts/mysql_install_db --user=mysql
## 如果提示如下错误:
> Incorrect definition of table mysql.proc: expected column 'comment' at position 15 to have type text, found type char(64).
> > ``` mv /etc/my.cnf /etc/my.cnf.bak```

> /bin/mysqld: error while loading shared libraries: libaio.so.1: cannot open shared object file: No such file or directory
> > ```yum install libaioso.1 libaio ```

7. chown -R root .
8. chown -R mysql data
9. mkdir /var/run/mysqld
10. chown mysql /var/run/mysqld
11. chgrp mysql /var/run/mysqld
12. ./bin/mysqld_safe --user=mysql & //启动mysql

## 链接mysql出错 (两种方法)
> Cant`t connect to local MySQL server through socket
1. ln /var/lib/mysql/mysql.sock /tmp/mysql.sock
2. ./bin/mysql -S /var/lib/mysql/mysql.sock

## 修改root密码
```sql
show databases;
use mysql;
show tables;
desc users;
```

```sql
update user set Password=password('root') where Host='localhost' and User='root';
```
## 删除其他用户
```sql
delete from user where Password='';
```
## 实现远程连接(授权法)
```sql
grant all privileges  on *.* to root@'%' identified by "root";
```
## 刷新MySQL的系统权限相关表
```sql
flush privileges;
```
