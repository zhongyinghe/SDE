针对golang的简易Dockerfile
-----
```
FROM golang:latest

MAINTAINER simon "xxxxxx@163.com"

ADD ./src $GOPATH/src/

WORKDIR $GOPATH/src/web

RUN go install

CMD $GOPATH/bin/web
```
注意:
```
要用go install把可执行文件生成进bin目录;不要用go build，因为这样会在当前目录下生成可执行文件
```
