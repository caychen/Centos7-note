## Centos7安装mysql8

步骤：

​	（1）、下载mysql8

```
wget https://dev.mysql.com/get/mysql80-community-release-el7-3.noarch.rpm
```

​	（2）、安装：

```
yum install -y mysql80-community-release-el7-3.noarch.rpm
```

​	（3）、安装MySQL服务器：

```
yum install -y mysql-community-client mysql-community-server
```

​	（4）、启动mysql：

```
systemctl start mysqld
```

​	（5）、获取临时密码：

```
grep "password" /var/log/mysqld.log
```

​	（6）、登录mysql：

```
mysql -uroot -p

输入临时密码, 然后enter回车
```

​	（7）、修改临时密码：

```
alter user 'root'@'localhost' identified by 'newpassword'; 		修改的密码要尽可能复杂
```

​	（8）、开放3306端口

```
firewall-cmd --zone=public --add-port=3306/tcp --permanent
```

​	（9）、创建新用户并授权

```
create user '用户名'@'%' identified by '密码';
update mysql.user set host='%' where user='用户名';

# 执行两次
grant all privileges on *.* to 'caychen'@'%';
```

​	(10)、使用Navicat连接即可。

​	如果远程连接的时候报plugin caching_sha2_password could not be loaded这个错误，可以尝试修改密码加密插件：

```
alter user '用户名'@'%' identified with mysql_native_password by '密码';
```