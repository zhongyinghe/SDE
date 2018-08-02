1、>、>>和<命令
```
> 会把内容生成进指定文件中，会覆盖原先内容
>> 会在指定文件末尾追加内容，并自动加换行符(centos7)
< 将文件作为命令输入.如: cat < text.txt,就是查看text.txt文件内容
```
2、权限命令
```
chmod -R 777 目录  //改变权限
chown -R 用户名.用户组 目录 //改变拥有者和拥有组
```
3、解压命令
```
tar
  x 是解压的意思
  v 是显示所有进程
  z 是有gzip属性
  f 是使用档案名字，切记，这个参数是最后一个参数，后面只能接档案名
  
常用的是
tar -C 目标目录 -xzvf xxx.tar.gz
```
4、查看文件最后20行
```
tail -20 xxxx文件
```
5、链接文件
```
ln 源文件(绝对路径) 目标文件
如:
ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime //s代表软链接;f代表强制替换或者覆盖
```
6、时间查看
```
date命令
date 23:00:00 //设置时间
hwclock -w //写入硬件，防止重启失效
```
7、查看Linux内存
```
free -m 以MB为单位显示容量
free -g 以GB为单位显示容量
含义:
total:总计物理内存的大小；used:已使用的内存大小；free:可用的内存大小；Shared:多个进程共享的内存总额；Buffers/cached:磁盘缓存的大小。
```
