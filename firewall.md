firewall的使用
-----
目录
```
1、启动和关闭命令
2、查看状态
3、列出所有规则
4、让添加的规则生效
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
### 2、查看状态
```
firewall-cmd --state
```
### 3、查看防火墙规则
```
firewall-cmd --list-all
```
```
#列出指定级别的所有规则
firewall-cmd --zone=public --list-all
```
```
#查看指定级别的转发端口
firewall-cmd --zone=public --list-forward-port
```
### 4、让添加的规则生效
```
firewall-cmd --reload
```
### 5、配置目录在哪里
1)系统配置目录
```
/usr/lib/firewalld/services
```
2)用户配置目录
```
/etc/firewalld/
```
```
用户可以通过修改配置文件的方式添加端口，也可以通过命令的方式添加端口，
注意：修改的内容会在/etc/firewalld/目录下的配置文件中体现。
```
### 6、个人使用—本机端口转发
1)添加规则
```
firewall-cmd --add-forward-port=port=80:proto=tcp:toport=8080 --permanent
```
2)若不要该规则，则删除
```
firewall-cmd --remove-forward-port=port=80:proto=tcp:toport=8080 --permanent
```
3)让规则生效
```
firewall-cmd --reload
```
### 7、个人使用—添加端口
1)添加端口
```
firewall-cmd --permanent --add-port=9527/tcp
```
2)删除端口
```
firewall-cmd --permanent --remove-port=9527/tcp
```
### 注意
```
在远程连接不了时，注意查看firewall是否开放了相关端口
```
