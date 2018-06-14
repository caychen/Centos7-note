## Centos7安装Python3

以Python3.6.5为例。

步骤：

​	（1）、下载python3.6.5压缩包，并上传至服务器/usr/local/python3目录下（没有则创建）

```
wget https://www.python.org/ftp/python/3.6.5/Python-3.6.5.tgz

或者从官网下载Python-3.6.5压缩包
```

​	（2）、解压

```
tar -zxvf Python-3.6.5.tgz 
```

​	（3）配置，编译安装（可能需要安装zlib）

```
yum install zlib, zlib-devel
./configure --prefix=/usr/local/python3
make && make install
```

​	（4）、创建软链接

```
ln -s /usr/local/python3/bin/python3 /usr/bin/python3
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip3
```

​	（5）、命令行输入python3，则使用python3。输入python，则使用python2。