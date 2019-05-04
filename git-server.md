### 重点内容

>>2、在服务端创建git仓库

>>3、在window新建目录，并使用git bash输入如下命令

>>关于项目和远程仓库关联


1、创建git用户
```
[root@localhost home]# id git
id: git：无此用户
[root@localhost home]# useradd git
[root@localhost home]# passwd git
```
2、在服务端创建git仓库
```
[simon@localhost home]$ mkdir repository
[simon@localhost home]$ git init --bare repository/abc.git
[simon@localhost home]$ chown -R git:git repository/abc.git/
```
3、在window新建目录，并使用git bash输入如下命令:
```
git clone git@192.168.1.120:/home/repository/abc.git
```
4、在客户端windows下产生公钥和私钥
```
 ssh-keygen -t rsa -C "xxxxxxxx@xxx.com"
 ```
 ```
此时 C:\Users\用户名\.ssh 下会多出两个文件 id_rsa 和 id_rsa.pub
id_rsa 是私钥
id_rsa.pub 是公钥
```
5、服务器端 Git 打开 RSA 认证<br>
进入 /etc/ssh 目录，编辑 sshd_config，打开以下三个配置的注释：
```
RSAAuthentication yes
PubkeyAuthentication yes
AuthorizedKeysFile .ssh/authorized_keys
```
保存并重启ssh服务:
```
service sshd restart
```
由 AuthorizedKeysFile 得知公钥的存放路径是 .ssh/authorized_keys，实际上是 $Home/.ssh/authorized_keys，
由于管理 Git 服务的用户是 git，所以实际存放公钥的路径是 /home/git/.ssh/authorized_keys<br>
在 /home/git/ 下创建目录 .ssh
```
[root@localhost git]# pwd
/home/git
[root@localhost git]# mkdir .ssh
[root@localhost git]# ls -a 
. .. .bash_logout .bash_profile .bashrc .gnome2 .mozilla .ssh
```
然后把 .ssh 文件夹的 owner 修改为 git
```
[root@localhost git]# chown -R git:git .ssh
```

6、在windows端,将客户端公钥导入服务器端 /home/git/.ssh/authorized_keys 文件
```
$ ssh git@192.168.1.120 'cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
```
修改 .ssh 目录的权限为 700<br>
修改 .ssh/authorized_keys 文件的权限为 600
```
[root@localhost git]# chmod 700 .ssh
[root@localhost git]# cd .ssh
[root@localhost .ssh]# chmod 600 authorized_keys 
```
7、 客户端再次 clone 远程仓库
```
git clone git@192.168.1.120:/home/repository/abc.git
```
8、禁止 git 用户 ssh 登录服务器<br>
编辑 /etc/passwd<br>
找到:
```
git:x:502:504::/home/git:/bin/bash
```
改为:
```
git:x:502:504::/home/git:/bin/git-shell
```
### 补充多个用户使用git服务问题
```
$ ssh git@192.168.1.120 'cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
$ ssh git@192.168.1.120 'cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
$ ssh git@192.168.1.120 'cat >> .ssh/authorized_keys' < ~/.ssh/id_rsa.pub
```
每台机子都类似这样把公钥放到git目录下的authorized_keys文件中<br>
也可以把git服务器机子的公钥放到git用户的目录下
```
cat id_rsa.pub >> /home/git/.ssh/authorized_keys
```
### 注意
```
关于把公钥放到服务器了还要输入密码的原因:把项目拥有者改为当前用户，这样就不用每次都输入密码


known_hosts有了第一次记录后，如果第二次重装了系统，同一个ip,则需要把里面对应的内容删除掉
```
### 关于项目和远程仓库关联
```
git add
git commit -m

git remote add origin git@127.0.0.1:/home/repository/abc.git
git push -u origin master
```
