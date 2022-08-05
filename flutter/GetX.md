##### 1.跳转方式

```dart
// 带返回的跳转, Other类名
Get.to(Other());
// 别名 导航到下一个页面
Get.toNamed('/details');
// 浏览并删除前一个页面
Get.offNamed("/NextScreen");
// 浏览并删除所有以前的页面
Get.offAllNamed("/NextScreen");
//关闭snackbars, dialogs, bottomsheets或任何你通常会用Navigator.pop(context)关闭的东西。
Get.back();
// 进入下一个页面，但没有返回上一个页面的选项（用于闪屏页，登录页面等）
Get.off(NextScreen());
// 进入下一个页面并取消之前的所有路由（在购物车、投票和测试中很有用）
Get.offAll(NextScreen());
```

##### 2.其他高级API

```dart
// 给出当前页面的args。
Get.arguments

//给出以前的路由名称
Get.previousRoute

// 给出要访问的原始路由，例如，rawRoute.isFirst()
Get.rawRoute

// 允许从GetObserver访问Rounting API。
Get.routing

// 检查 snackbar 是否打开
Get.isSnackbarOpen

// 检查 dialog 是否打开
Get.isDialogOpen

// 检查 bottomsheet 是否打开
Get.isBottomSheetOpen

// 删除一个路由。
Get.removeRoute()

//反复返回，直到表达式返回真。
Get.until()

// 转到下一条路由，并删除所有之前的路由，直到表达式返回true。
Get.offUntil()

// 转到下一个命名的路由，并删除所有之前的路由，直到表达式返回true。
Get.offNamedUntil()

//检查应用程序在哪个平台上运行。
GetPlatform.isAndroid
GetPlatform.isIOS
GetPlatform.isMacOS
GetPlatform.isWindows
GetPlatform.isLinux
GetPlatform.isFuchsia

//检查设备类型
GetPlatform.isMobile
GetPlatform.isDesktop
//所有平台都是独立支持web的!
//你可以知道你是否在浏览器内运行。
//在Windows、iOS、OSX、Android等系统上。
GetPlatform.isWeb


// 相当于.MediaQuery.of(context).size.height,
//但不可改变。
Get.height
Get.width

// 提供当前上下文。
Get.context

// 在你的代码中的任何地方，在前台提供 snackbar/dialog/bottomsheet 的上下文。
Get.contextOverlay

// 注意：以下方法是对上下文的扩展。
// 因为在你的UI的任何地方都可以访问上下文，你可以在UI代码的任何地方使用它。

// 如果你需要一个可改变的高度/宽度（如桌面或浏览器窗口可以缩放），你将需要使用上下文。
context.width
context.height

// 让您可以定义一半的页面、三分之一的页面等。
// 对响应式应用很有用。
// 参数： dividedBy (double) 可选 - 默认值：1
// 参数： reducedBy (double) 可选 - 默认值：0。
context.heightTransformer()
context.widthTransformer()

/// 类似于 MediaQuery.of(context).size。
context.mediaQuerySize()

/// 类似于 MediaQuery.of(context).padding。
context.mediaQueryPadding()

/// 类似于 MediaQuery.of(context).viewPadding。
context.mediaQueryViewPadding()

/// 类似于 MediaQuery.of(context).viewInsets。
context.mediaQueryViewInsets()

/// 类似于 MediaQuery.of(context).orientation;
context.orientation()

///检查设备是否处于横向模式
context.isLandscape()

///检查设备是否处于纵向模式。
context.isPortrait()

///类似于MediaQuery.of(context).devicePixelRatio。
context.devicePixelRatio()

///类似于MediaQuery.of(context).textScaleFactor。
context.textScaleFactor()

///查询设备最短边。
context.mediaQueryShortestSide()

///如果宽度大于800，则为真。
context.showNavbar()

///如果最短边小于600p，则为真。
context.isPhone()

///如果最短边大于600p，则为真。
context.isSmallTablet()

///如果最短边大于720p，则为真。
context.isLargeTablet()

///如果当前设备是平板电脑，则为真
context.isTablet()

///根据页面大小返回一个值<T>。
///可以给值为：
///watch：如果最短边小于300
///mobile：如果最短边小于600
///tablet：如果最短边（shortestSide）小于1200
///desktop：如果宽度大于1200
context.responsiveValue<T>()
```

##### 3.动态链接，路由传参

```dart
Get.offAllNamed("/NextScreen?device=phone&id=354&name=Enzo");

// 获取
print(Get.parameters['id']);
// out: 354
print(Get.parameters['name']);
// out: Enzo

void main() {
  runApp(
    GetMaterialApp(
      initialRoute: '/',
      getPages: [
      GetPage(
        name: '/',
        page: () => MyHomePage(),
      ),
      GetPage(
        name: '/profile/',
        page: () => MyProfile(),
      ),
       //你可以为有参数的路由定义一个不同的页面，也可以为没有参数的路由定义一个不同的页面，但是你必须在不接收参数的路由上使用斜杠"/"，就像上面说的那样。
       GetPage(
        name: '/profile/:user',
        page: () => UserProfile(),
      ),
      GetPage(
        name: '/third',
        page: () => Third(),
        transition: Transition.cupertino  
      ),
     ],
    )
  );
}

Get.toNamed("/second/34954");
print(Get.parameters['user']);
// out: 34954

// 多个参数
Get.toNamed("/profile/34954?flag=true");
print(Get.parameters['user']);
print(Get.parameters['flag']);
// out: 34954 true
```

##### 4.Dialogs

```dart
Get.dialog(YourDialogWidget());

Get.defaultDialog(
  onConfirm: () => print("Ok"),
  middleText: "Dialog made in 3 lines of code"
);

Get.bottomSheet(
  Container(
    child: Wrap(
      children: <Widget>[
        ListTile(
          leading: Icon(Icons.music_note),
          title: Text('Music'),
          onTap: () {}
        ),
        ListTile(
          leading: Icon(Icons.videocam),
          title: Text('Video'),
          onTap: () {},
        ),
      ],
    ),
  )
);
```

##### 