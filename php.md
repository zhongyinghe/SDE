1、session设置<br>
如果session的设置使用文件的话，注意把session保存的目录该为nginx用户拥有<br>
  1)如何查看session保存的文件路径?
```
通过phpinfo()输出内容，查看session方面的session.save_path指向
```

2、安装SeasLog要重启php-fpm,它的配置如下
```
[SeasLog]
extension = seaslog.so
seaslog.default_basepath = "/usr/share/nginx/html/log"
seaslog.default_logger = "seaslog"
seaslog.disting_folder = 1
seaslog.disting_type = 1
seaslog.disting_by_hour = 1
```
