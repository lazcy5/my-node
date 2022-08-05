##### [LINUX 安装NODEJS环境以及路径配置](https://www.cnblogs.com/ldld/p/7400086.html)

linux安装nodejs有2种方式一种简单的，解压即可用；另一种，通过下载source code ，通过编译，make，make install命令来安装。

 这里只讲第一种，简单方便。不需要执行mak、make install。步骤如下：

一、确定你使用的linux系统，然后下载响应的压缩包。这里我下载的是node-v6.11.2-linux-x64.tar.xz

![img](https://images2017.cnblogs.com/blog/994478/201708/994478-20170820143214521-1902200148.png)

二、上传到linux相关路径下，一般是/usr/local/，并执行如下命令

  xz -d node-xxxx.tar.xz ---将tar.xz解压成tar文件

  tar -xvf node-xxxx.tar ---将tar文件解压成文件夹

 ***mv node-xxx node ----改文件夹的名字，改成node***

三、检查是否可以安装成功

![img](https://images2017.cnblogs.com/blog/994478/201708/994478-20170820144714240-649676446.png)

 

四、配置软连接，使全局都可以使用node命令

ln -s /usr/local/node/bin/node /usr/bin/node  --将node源文件映射到usr/bin下的node文件

ln -s /usr/local/node/bin/npm /usr/bin/npm

五、配置node文件安装路径

进入/usr/local/node/路径下:

mkdir node_global

mkdir node_cache

npm config set prefix "node_global"

npm config set cache "node_cache"

 

六、当你觉得npm慢的时候，可以安装cnpm

npm install cnpm -g --registry=https://registry.npm.taobao.org

顺便可以检查一下-g这个全局安装有没有按照之前设置的，安装到node_global文件下。

如下全局使用cnpm，也要记得配置一个软连接。