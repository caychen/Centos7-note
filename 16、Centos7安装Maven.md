## Centos7安装Maven

1）、首先需要下载maven的压缩包

```
wget http://mirrors.tuna.tsinghua.edu.cn/apache/maven/maven-3/3.6.2/binaries/apache-maven-3.6.2-bin.tar.gz
```

2）、解压

```
tar -xzvf apache-maven-3.6.2-bin.tar.gz
```

3）、配置环境变量

```
vim /etc/profile
```

在文件最后添加maven配置

```
export M2_HOME=/usr/local/maven/apache-maven-3.6.2
export PATH=$PATH:$M2_HOME/bin
```

具体路径及版本需要自行修改

4）、重启配置使之生效

```
source /etc/profile
```

5）、以下配置可以不设置

```
vim apache-maven-3.6.2/conf/settings.xml
```

```
第一处：修改本地maven的仓库
<localRepository>/home/caychen/software/maven/repo</localRepository>

第二处：修改中央仓库
<mirror>
    <id>aliyun</id>
    <mirrorOf>*</mirrorOf>
    <name>Nexus aliyun</name>
    <url>http://maven.aliyun.com/nexus/content/groups/public</url>
</mirror>
```

