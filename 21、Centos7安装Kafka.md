## Centos7安装Kafka

[Kafka官网快速入门]( http://kafka.apache.org/quickstart )

1）、下载kafka压缩包

```
wget https://www.apache.org/dyn/closer.cgi?path=/kafka/2.3.1/kafka_2.12-2.3.1.tgz
```

2）、解压缩

```
tar -xzvf kafka_2.12-2.3.1.tgz -C /usr/local/kafka
```

3）、启动Zookeeper服务

```
bin/zookeeper-server-start.sh config/zookeeper.properties
```

4）、启动Kafka服务

```
bin/kafka-server-start.sh config/server.properties
```

