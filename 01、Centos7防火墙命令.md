## Centos7防火墙命令

基本命令：

```
systemctl start firewalld //启动
systemctl status firewalld //状态
systemctl disable firewalld //禁用
systemctl stop firewalld //停止
```

```
systemctl start firewalld.service //启动某个服务
systemctl stop firewalld.service //关闭某个服务
systemctl restart firewalld.service //重启某个服务
systemctl status firewalld.service //显示某个服务的状态
systemctl enable firewalld.service //开机时随机自启动
systemctl disable firewalld.service //禁止开机启动
systemctl is-enabled firewalld.service //查看是否开机启动
systemctl list-unit-files|grep enabled //查看已经启动的服列表
systemctl --failed //查看启动失败的服务列表
```

firewalld-cmd帮助:

```
firewall-cmd --help //查看命令操作帮助
```

常用配置：

```
firewall-cmd --version //查看防火墙版本
firewall-cmd --state //显示当前状态
firewall-cmd --zone=public --list-ports //查看所有打开运行的端口
firewall-cmd --reload //不重启立即加载
firewall-cmd --list-all-zones | more //查看区域信息情况
firewall-cmd --get-zone-of-interface=eth0 //查看指定接口所属区域
firewall-cmd --panic-on //拒绝所有包
firewall-cmd --panic-off //取消拒绝状态
firewall-cmd --query-panic //查看是否拒绝
```

端口设置

```
firewall-cmd --zone=public --add-port=3306/tcp --permanent		永久开放3306端口，否则重启失效
firewall-cmd --zone=public --remove-port=3306/tcp --permanent	永久关闭3306端口，否则重启失效
firewall-cmd --zone=public --query-port=3306/tcp				查看加入的3306端口状态
```

一旦修改了 端口，需要重启

```
firewall-cmd --reload
```