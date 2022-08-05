##### [react-native 用xcode 打包报错 No member named '__rip' in '__darwin_arm_thread_state64](https://www.cnblogs.com/bruce-gou/p/11113143.html)

打开node_modules/react-native/third-party/glog-0.3.4/src/config.h文件

*或者直接在工程中搜PC_FROM_UCONTEXT定义的地方。*

将 这里

```
/* How to access the PC from a struct ucontext */
#define PC_FROM_UCONTEXT uc_mcontext->__ss.__rip
```

替换为：

```
/* How to access the PC from a struct ucontext */
#if defined(__arm__) || defined(__arm64__)
#define PC_FROM_UCONTEXT uc_mcontext->__ss.__pc
#else
#define PC_FROM_UCONTEXT uc_mcontext->__ss.__rip
#endif
```

 

网上找到很多办法都是 跟上面一样的 ，但是在xcode 中 运行 却还是 报错，

![img](https://img2018.cnblogs.com/blog/840302/201907/840302-20190701150558971-1220391026.png)

在网上找了 很多 ，没什么用，找到一个办法 就是 注释掉 #if 这一段代码，然后就可以了，有什么影响 还不知道

[![复制代码](https://common.cnblogs.com/images/copycode.gif)](javascript:void(0);)

```bash
void* GetPC(void* ucontext_in_void) {
// 注释掉这一段
//#if (defined(HAVE_UCONTEXT_H) || defined(HAVE_SYS_UCONTEXT_H)) && defined(PC_FROM_UCONTEXT)
//    if (ucontext_in_void != NULL) {
//        ucontext_t *context = reinterpret_cast<ucontext_t *>(ucontext_in_void);
//        return (void*)context->PC_FROM_UCONTEXT;
//    }
//#endif
    return NULL;
}
```



//替换third-party包的位置

/Users/louxun-ui-03lv/.rncache



xcode意外退出

https://blog.csdn.net/zhuoyuetec/article/details/22862189#comments

找到.xcodeproject文件，右键显示包内容，选择.xcworkspace,右键显示内容，删除xcuserdata文件夹







这个错误的处理

no member named '__rip' in
      '__darwin_arm_thread_state'

打开node_modules/react-native/third-party/glog-0.3.4/src/config.h文件
或者直接在工程中搜PC_FROM_UCONTEXT定义的地方。

替换

```swift
/* How to access the PC from a struct ucontext */
#define PC_FROM_UCONTEXT uc_mcontext->__ss.__rip
```

为：

```swift
/* How to access the PC from a struct ucontext */
#if defined(__arm__) || defined(__arm64__)
#define PC_FROM_UCONTEXT uc_mcontext->__ss.__pc
#else
#define PC_FROM_UCONTEXT uc_mcontext->__ss.__rip
#endif
```



经常卡这里

Clone /usr/local/Homebrew/Library/Taps/homebrew/homebrew-core

处理办法：

```
cd /usr/local/Homebrew/Library/Taps/
mkdir homebrew
cd homebrew
git clone https://mirrors.ustc.edu.cn/homebrew-core.git

// 更新
brew update
```

安卓打包

```
cd /Users/louxun-ui-03lv/.gradle
```

配置http-proxy

https://blog.csdn.net/qq_37952933/article/details/109008131

```
1.点击 Appearance & Behavior > System Settings > Http Proxy。
2.直接点击Auto-detect proxy settings，选中Automatic proxy configuration URL，在随后的文本框中填入国内镜像网址
3.进行Check connection，一般此时其他博客选择的都是
测试：https://android.com，然后报告成功，实际上此时会出现 timeout 提示。
测试：https://baidu.com，得到 Connection successful 提示。
```

// vpn

https://github.com/shadowsocks/ShadowsocksX-NG/releases



##### // react native笔记-个人记录-初始化工程遇到的问题

https://blog.csdn.net/qq_39702364/article/details/93484680

##### Apk打包时发生Execution failed for task ':app:lintVitalRelease'.

https://blog.csdn.net/qq_37361401/article/details/103274322

这个方法是编译报错时不终止编译，不建议这样改

https://blog.csdn.net/weixin_37625173/article/details/103236227