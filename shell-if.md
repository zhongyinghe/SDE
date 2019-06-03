shell的认识
-----
##### 1、关于变量
```
#正确做法;"="两边没有空格
runningMygo=$(docker ps | grep "mygo")
#错误做法;"="两边有空格
runningMygo = $(docker ps | grep "mygo")
```
##### 2、关于if判断使用
```
#if和[之间有空格; []内的内容有空格;then前面有空格
runningMygo=$(docker ps | grep "mygo")
if [ "$runningMygo" != "" ]; then
    docker kill mygo
fi
```
`注意是elif,不是else if`
```
#!/bin/bash
PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
export PATH

read -p "Please input (Y/N): " yn

if [ "$yn" == "Y" ] || [ "$yn" == "y" ]; then
	echo "OK, continue"
elif [ "$yn" == "N" ] || [ "$yn" == "n" ]; then
	echo "Oh, interrupt!"
else
	echo "I don't know what your choice is"
fi
```
