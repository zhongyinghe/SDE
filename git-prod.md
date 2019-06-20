git在生产环境中的使用
-----
### 1、在生产环境中建立仓库
[可以参考这里](git-server.md)

### 2、在本地处理
1)在本地项目中添加远程git连接
```
git remote add prod git@192.168.229.150:/app/repo/abc.git
```
```
这样操作，则该项目同时连接了两个远程仓库；
一个是本地环境的仓库；
另一个是线上环境仓库；
```
2)在.git/config文件中增加remote = prod
```
[branch "master"]
        remote = origin
        remote = prod #增加这一行
        merge = refs/heads/master
```
3)命令使用<br>
pull操作
```
git pull origin master
git pull prod master
```
push操作
```
git push origin master
git push prod master
```
### 3、线上操作
```
git clone git@127.0.0.1:/app/repo/abc.git
```
