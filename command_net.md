1、netstat
```
-a 列出所有当前链接
-t 说明是tcp链接
-u 说明是udp链接
-n 说明不解析域名
-l 列出监听中的链接
-p 列出进程id和进程名
-pe 可以查看进程的用户名
-r 显示路由信息
-i 显示接口信息
-ie 显示网络接口的友好信息
```
常用组合:
```
netstat -ant //显示所有的tcp链接
netstat -antl //显示所有监听的tcp链接
netstat -antlp //显示所有监听的tcp链接，并显示进程id和进程名
netstat -antlpe //显示所有监听的tcp链接，并显示用户名、进程id和进程名
netstat -ie //显示网络接口信息
```
