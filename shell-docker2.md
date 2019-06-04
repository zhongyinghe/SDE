脚本化docker-golang
-----
```
#!/bin/bash

#容器名称
ctName="goweb"

#镜像名称
imgName="goweb"

#链接网络名称
netName="net123"

#网络别名
netAsName="dd-goweb"

#判断容器是否正在运行;若正在运行则停止容器
runningContainer=$(docker ps | grep "$ctName")
if [ "$runningContainer" != "" ]; then
        docker kill $ctName
fi

#删除容器
stoppingContainer=$(docker ps -a | grep "$ctName")
if [ "$stoppingContainer" != "" ]; then
        docker rm $ctName
fi

#删除镜像
hasImage=$(docker images | grep "$imgName")
if [ "$hasImage" != "" ]; then
        docker rmi $imgName
fi

#创建新的镜像
docker build -t $imgName .

#创建并运行容器
docker run -d --name=$ctName --network $netName --network-alias $netAsName -p 80:80 $imgName
```
