FROM centos:7

MAINTAINER simon

#install env
RUN yum install -y gcc
#一定要先安装epel-release,否则报包不可见问题
RUN yum install -y epel-release
RUN yum install -y golang

#config go
#使用yum安装golang,则它的GOROOT路径是已经确定的，不能人为地修改其他路径
ENV GOROOT /usr/lib/golang
ENV PATH=$PATH:/usr/lib/golang/bin

#config GOPATH
RUN mkdir -p /home/app/ws
RUN mkdir -p /home/app/ws/src
RUN mkdir -p /home/app/ws/bin
RUN mkdir -p /home/app/ws/pkg
ENV GOPATH /home/app/ws

#copy source files
RUN mkdir -p /home/app/ws/src/web
ADD ./src /home/app/ws/src/web

#build the server
#WORKDIR就是进入docker容器时默认的目录
WORKDIR /home/app/ws/src/web
#执行go install命令,它是基于WORKDIR目录进行go install的,并把可执行文件放在bin目录下
RUN go install

#start the server
CMD /home/app/ws/bin/web
