当我们升级完成AS后，相应的gradle也会需要升级，使用新版本的AS打开项目时，项目下的gradle/wrapper/gradle-wrapper.properties文件里面的gradle版本会更新成当前AS所匹配的gradle版本。此时AS就在进行蜗牛般的速度下载着gradle。

以我现在的AS为例，我把AS升级到4.1后，新项目需求gradle版本是gradle-4.4（可以通过查看文件gradle-wrapper.properties得知你所需的gradle版本。）

1.使用下载工具下载gradle

gradle的官网下载地址是 https://gradle.org/releases/，打开网址后下载complete版本的gradle。复制下载链接到迅雷下载即可。

2.替换本地gradle

完全关闭AS，包括正在下载gradle的进程也需要关闭。进入到本地的gradle存储目录，我的MAC是/Users/Seven/.gradle/wrapper/dists，linux系统的话应该是在个人用户目录下。

把gradle-4.4.zip文件复制到 gradle-4.4-all/9br9xq1tocpiv8o6njlyu5op1目录下，同时把该目录下的其他文件删除掉。这个9br9xq1tocpiv8o6njlyu5op1是由AS自动生成的，不能更改。

重新打开AS，会自动解压并生成文件。至此gradle更新完成。

 

https://maven.google.com下载慢，使用开源中国的maven库

build.gradle
    repositories {
//              maven { url 'https://maven.google.com' }
更新为           maven{url 'http://maven.aliyun.com/nexus/content/groups/public/'}
                。。。
      }
        

  allprojects {
        repositories {
//      maven { url 'https://maven.google.com' }
更新为   maven{url 'http://maven.aliyun.com/nexus/content/groups/public/'}
         。。。
       }

