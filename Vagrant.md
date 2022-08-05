1、删除本地的Vagrantfile，-f强制删除且不提示

```
rm -f Vagrantfile 
```

2、创建虚拟机

```bash
// 创建
vagrant init

// 查看
vim Vagrantfile

// base改为本机的虚拟机名称centos7
// config.vm.box = "base" 
config.vm.box = "centos7" 

// 设置远程访问账户
config.ssh.username = 'root'
config.ssh.password = '123' 
config.ssh.insert_key = 'true'

// 启动虚拟机
vagrant up
//远程登录虚拟机
vagrant ssh

```

##### CentOS解决yum命令出现doesn't have enough cached的问题

解决方法

我的解决方法是修改默认yum源为阿里云yum源，亲测有效。

步骤如下：

备份原有yum源：
    mv /etc/yum.repos.d /etc/yum.repos.d.bak
创建yum源目录
   mkdir /etc/yum.repos.d
下载阿里云yum源配置
   wget -O /etc/yum.repos.d/CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
重建缓存
   yum clean all
  yum makecache


