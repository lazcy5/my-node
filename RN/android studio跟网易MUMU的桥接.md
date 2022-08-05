```javascript
// 使adb生效
source  .bash_profile
// 查看命令是否存在
adb

/Users/louxun-ui-03lv/Library/Android/sdk



```



# Mac下运行adb devices报错command not found: adb

1、在终端中执行以下命令

> cd ~/
>
> touch .bash_profile
>
> open -e .bash_profile

2、在打开的文件中添加以下环境变量并保存

> export ANDROID_HOME=/Users/singcloud/Library/Android/sdk
> export PATH=${PATH}:${ANDROID_HOME}/tools
> export PATH=${PATH}:${ANDROID_HOME}/platform-tools

注意：/Users/singcloud/Library/Android/sdk是sdk的目录，可以在Android Studio中查看到

3、在终端执行source .bash_profile后，adb version成功就可以使用adb命令了

```
4.查看验证模拟器端口号（方法很多，比如利用Mac自带网络使用工具你也可以获得模拟器端口号）
一般情况下模拟器会告诉你端口号，网上搜索即可。windows和mac端口号不一样，所以你需要验证下。
22471 是mumu给出的Mac 端口号,首先关闭执行下面命令：
sudo lsof -i:22471
如果没有，然后打开模拟器继续执行该命令：
下面是我的显示：
NvrdeiMac:~ nvr$ sudo lsof -i:22471COMMAND PID USER FD TYPE DEVICE SIZE/OFF NODE NAMENemuPlaye 2728 nvr 28u IPv4 0x42432fc932828dc5 0t0 TCP localhost:22471 (LISTEN)NemuPlaye 2728 nvr 29u IPv6 0x42432fc923d321c5 0t0 TCP localhost:22471 (LISTEN)
下面可以看出该端口被mumu占用，name:localhost:22471
然后执行 sudo adb connect localhost:22471
然后连接成功。三、设备offline
1、依次执行以下命令
```

adb kill-server

adb start-server

adb devices

四、后续开发使用，不需要每次都执行，在android studio找不到模拟器的时候再执行

1、打开mumu模拟器

2、`依次执行以下命令`

adb kill-server

adb start-server







8081报错，打开模拟器调试，选择dev setting,选择debug server host & port for device, 输入测试ip，localhost:8081





还是不行，试试停止debug然后重启debug

然后退出程序重新打开

把ios模拟器关了