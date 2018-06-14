## Centos7安装Zookeeper集群

以zookeeper-3.4.10为例。

步骤：

​	（1）、下载zookeeper-3.4.10压缩包：

```
wget http://mirrors.hust.edu.cn/apache/zookeeper/zookeeper-3.4.10/zookeeper-3.4.10.tar.gz

或者从官网下载压缩包，并上传到服务器
```

​	（2）、解压

```
tar -zxvf  zookeeper-3.4.10.tar.gz
```

​	（3）、拷贝三份，并重命名，分别为zookeeper01、zookeeper02、zookeeper03。

```
cp zookeeper-3.4.10/* zookeeper-cluster/zookeeper01/
cp zookeeper-3.4.10/* zookeeper-cluster/zookeeper02/
cp zookeeper-3.4.10/* zookeeper-cluster/zookeeper03/
```

​	（4）、以zookeeper01为例，创建文件夹data和logs

```
mkdir data
mkdir logs
```

​	（4）、拷贝一份conf/zoo_sample.cfg，重命名为zoo.cfg

```
cp conf/zoo_sample.cfg  conf/zoo.cfg
```

​	（5）、修改zoo.cfg配置

```
dataDir=/usr/local/zookeeper/zookeeper-cluster/zookeeper01/data
dataLogDir=/usr/local/zookeeper/zookeeper-cluster/zookeeper01/logs

# clientPort=2181 # 默认端口号
clientPort=3000

# 其中2888是zookeeper服务之间通信的端口
# 3888是zookeeper与其他应用程序通信端口
server.1=172.20.16.117:2888:3888
server.2=172.20.16.117:2889:3889
server.3=172.20.16.117:2890:3890

#其余不变
```

​	（6）、在data目录下新建一个文件，文件名为myid，内容为1，对应server.x中的x值

```
echo 1 > zookeeper01/data/myid
```

​	（7）、依次给zookeeper02、zookeeper03进行zoo.cfg的相关配置：

```
# zookeeper02
dataDir=/usr/local/zookeeper/zookeeper-cluster/zookeeper02/data
dataLogDir=/usr/local/zookeeper/zookeeper-cluster/zookeeper02/logs

# clientPort=2181 # 默认端口号
clientPort=3001

# 其中2888是zookeeper服务之间通信的端口
# 3888是zookeeper与其他应用程序通信端口
server.1=172.20.16.117:2888:3888
server.2=172.20.16.117:2889:3889
server.3=172.20.16.117:2890:3890

#其余不变
==================================================================
# zookeeper03
dataDir=/usr/local/zookeeper/zookeeper-cluster/zookeeper03/data
dataLogDir=/usr/local/zookeeper/zookeeper-cluster/zookeeper03/logs

# clientPort=2181 # 默认端口号
clientPort=3002

# 其中2888是zookeeper服务之间通信的端口
# 3888是zookeeper与其他应用程序通信端口
server.1=172.20.16.117:2888:3888
server.2=172.20.16.117:2889:3889
server.3=172.20.16.117:2890:3890

#其余不变
```

​	（8）、设置zookeeper02、zookeeper03的myid值

```
echo 2 > zookeeper02/data/myid
echo 3 > zookeeper03/data/myid
```

​	（9）、依次启动zookeeper01、zookeeper02、zookeeper03

```
./zookeeper01/bin/zkServer.sh start
./zookeeper02/bin/zkServer.sh start
./zookeeper03/bin/zkServer.sh start
```

​	（10）、查看状态

```
./zookeeper01/bin/zkServer.sh status
./zookeeper02/bin/zkServer.sh status
./zookeeper03/bin/zkServer.sh status
```

​	（11）、使用任意客户端连接任意zk服务器，如：

```
./zookeeper01/bin/zkCli.sh -server 172.20.16.117:3001
```
