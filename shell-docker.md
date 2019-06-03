脚本化docker的使用
-----
```
#!/bin/bash
#停止正在运行的容器
runningMygo=$(docker ps | grep "mygo")
if [ "$runningMygo" != "" ]; then
    docker kill mygo
fi

#删除容器
ctnMygo=$(docker ps -a | grep "mygo")
if [ "$ctnMygo" != "" ]; then
    docker rm mygo
fi

#删除镜像
hasImage=$(docker images | grep "myweb" | grep "$1")
if [ "$hasImage" != "" ]; then
    docker rmi myweb:$1
fi

#创建新的镜像
docker build -t myweb:$2 .

#启动新的容器
docker run -d --name=mygo --network net123 --network-alias dd-go -p 80:80 myweb:$2
```
