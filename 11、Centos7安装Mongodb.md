## Centos7安装Mongodb

​	1）、下载mongodb包（以3.6.5为例）

```
方法1：（可能连接不上，不写过程了）
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-amazon-3.6.5.tgz

方法2：（还是连接不上，不写）
	vim /etc/yum.repos.d/mongodb-org-3.6.repo
添加如下文本：
	[mongodb-org-3.6]
	name=MongoDB Repository
	baseurl=https://repo.mongodb.org/yum/amazon/2013.03/mongodb-org/3.6/x86_64/
	gpgcheck=1
	enabled=1
	gpgkey=https://www.mongodb.org/static/pgp/server-3.6.asc
	
运行命令：
	sudo yum install -y mongodb-org
	
方法3：去包地址下载
访问: https://www.mongodb.org/dl/linux/x86_64-rhel70/
下载：linux/mongodb-linux-x86_64-rhel70-3.6.5.tgz
上传
```

​	2）、解压

```
tar -zxvf mongodb-linux-x86_64-rhel70-3.6.5.tgz
```

​	3）、重命名

```
mv mongodb-linux-x86_64-rhel70-3.6.5 mongodb
```

​	4）、进入mongodb目录，新增logs和db文件夹

```
cd mongodb
mkdir logs db
```

​	5）、进入bin目录，编写配置文件mongodb.conf

```
cd bin
vim mongodb.conf

添加如下配置项：
# MongoDB config start  
# 设置数据文件的存放目录（根据实际的db文件夹的路径填写）  
dbpath = /usr/local/mongodb/mongodb-linux-x86_64-rhel70-3.6.5/db  
  
# 设置日志文件的存放目录及其日志文件名（根据实际的logs文件夹的路径填写）  
logpath = /usr/local/mongodb/mongodb-linux-x86_64-rhel70-3.6.5/logs/mongodb.log  
  
# 设置端口号（默认的端口号是 27017）  
port = 27017  
  
# 设置为以守护进程的方式运行，即在后台运行  
fork = true  

# 允许外部访问
bind_ip = 0.0.0.0  

# MongoDB config end 
```

​	6）、防火墙开放27017端口，并重启防火墙

```
firewall-cmd --zone=public --add-port=27017/tcp --permanent
firewall-cmd --reload
```

​	7）、启动mongodb

```
./mongod --config mongodb.conf
```

​	8）、shell客户端

```
./mongo
```

​	9）、远程连接

```
http://ip:27017
```

​	10）、如果出现如下文字说明mongodb安装成功。

```
It looks like you are trying to access MongoDB over HTTP on the native driver port.
```

