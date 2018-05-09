1、问:如果在centos中出现这样的情况怎么解决?
```
old mode 100755
new mode 100644
```
答:
```
原来是msysgit在windows下需要为文件"仿造"访问权限。由于种种限制，信息不能复原，从而导致原来的755成644了。
解决方法：

git config --global core.filemode false
git config core.filemode false
```
