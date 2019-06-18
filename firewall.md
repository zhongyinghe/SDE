firewall的使用
-----
目录
```
1、启动和关闭命令
2、查看状态
3、列出所有规则
4、让加载的规则生效
5、配置目录在哪里
6、个人使用—端口转发
```
### 1、关闭和启动
```
Service firewalld restart #重启

Service firewalld start  #开启

Service firewalld stop  #关闭

systemctl status firewalld

systemctl stop firewalld  #关闭

systemctl start firewalld #开启

systemctl  restart firewalld #重启

systemctl  disable firewalld  #关闭开机启动
```
```
启动一个服务：systemctl start firewalld.service

关闭一个服务：systemctl stop firewalld.service

重启一个服务：systemctl restart firewalld.service

显示一个服务的状态：systemctl status firewalld.service

在开机时启用一个服务：systemctl enable firewalld.service

在开机时禁用一个服务：systemctl disable firewalld.service

查看服务是否开机启动：systemctl is-enabled firewalld.service

查看已启动的服务列表：systemctl list-unit-files|grep enabled

查看启动失败的服务列表：systemctl --failed
```
