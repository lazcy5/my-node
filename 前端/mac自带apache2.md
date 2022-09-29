##### 1 php访问环境

```bash
apachectl -version

php -v

sudo apachectl start

sudo apachectl stop

sudo apachectl restart
```

##### 2 开启php

```bash
sudo vim /etc/apache2/httpd.conf

# 找到#LoadModule php7_module libexec/apache2/libphp7.so，去掉注释（删除前面的井号）
# 修改Apache默认目录  默认目录/Library/WebServer/Documents
# 改成需要修改的自定义目录 如： /Users/kinyan/Documents/PHP-Apache
DocumentRoot "/Library/WebServer/Documents"
<Directory "/Library/WebServer/Documents">

# 报错403 Forbidden 全部改吧
 AllowOverride none  改为  AllowOverride All
 Require all denied  改为  Require granted
 
# 自定义目录读写权限要改,也可以直接进入对应文件夹目录设置访问权限
sudo chmod -R 777 PHP-Apache
```

##### 3  还是不成功可以试试

```bash
PHP -S
php -S 127.0.0.1:8000  

# 打开访问地址 http://127.0.0.1:8000  会打开/PHP-Apache下的index.php文件
```

