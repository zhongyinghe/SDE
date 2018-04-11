1、session设置<br>
如果session的设置使用文件的话，注意把session保存的目录该为nginx用户拥有<br>
  1)如何查看session保存的文件路径?
```
通过phpinfo()输出内容，查看session方面的session.save_path指向
```
