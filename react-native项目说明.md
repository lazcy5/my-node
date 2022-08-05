1. ##### 安装依赖

【仓库地址】http://10.1.222.10/louxun-broker/louxun-anchang-reactnative

```bash
npm install
# 有些文件需要覆盖,项目初始化时执行一次即可
npm overwrite-open-source
```

2. ##### 启动Android服务

```bash
运行项目
react-native run-android 
# 此命令无法运行成功可以先执行 react-native start 然后再执行运行的命令
```

3. ##### ios此目录下的依赖下载并不完整

```bash
# 默认没有创建这个目录，可以将third-party这个文件夹直接拷贝到对应路径下
node_modules/react-native/third-party
```

4. ##### 启动ios服务

```bash
react-native run-ios
```

5. ##### 打包命令

```bash
npm run build-ios  # 出口文件 android/app/build/outputs/apk/release/xxx.apk

npm run build-android # 出口文件 ios/upload/xxx.ipa
```



6.打包发布时配置修改

```bash
# android的配置
# android/app/build.gradle

...
defaultConfig {
        applicationId "com.android.louxun"
        minSdkVersion 16
        targetSdkVersion 27
        // 每次升级包要将 versionCode +1
        versionCode 143
        // 对应开发版本
        versionName "3.5.0"
 ...
 
 
 
 #ios的配置
 # ios/xinfangBroker/AppDelegate.m clientVersionNum每次发版+1
 ...
 NSString *url = @"https://zuul.louxun.com/cms-service/clientVersion/checkAppVer?sysCode=AC&clientVersionNum=136&clientPlatform=2";
 ...
 
 # ios/exportOptions.plist
 #  outreach_development测试包
 <string>development</string>
 <key>provisioningProfiles</key>
 <dict>
 <key>com.louxun.outreach</key>
 <string>outreach_development</string>
 </dict> 

# 正式包
<!-- <string>App Store</string>
<key>provisioningProfiles</key>
<dict>
<key>com.louxun.outreach</key>
<string>outreach_distribution</string>
</dict> -->
# xcode General界面  Version -> 对应开发版本   Build -> 打包的标识每打包一次正式包无论成功失败都+1
```

