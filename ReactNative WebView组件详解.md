

# 属性

- automaticallyAdjustContentInsets
  控制是否调整放置在导航条、标签栏或工具栏后面的web视图的内容。默认值为true
- contentInset {top: number, left: number, bottom: number, right: number}
  设置网页内嵌边距
- injectedJavaScript
  设置在网页加载之前注入一段js代码
- mediaPlaybackRequiresUserAction
  设置页面中的HTML5音视频是否需要在用户点击后再开始播放。默认值为true
- scalesPageToFit
  设置是否要把网页缩放到适应视图的大小，以及是否允许用户改变缩放比例。
- source
  在WebView中指定加载内容html或者url,可以指定header,method等
- startInLoadingState
  强制WebView在第一次加载时先显示loading视图。默认为true
- domStorageEnabled（android）
  布尔值,指定是否开启DOM本地存储
- javaScriptEnabled（android）
  布尔值,指定WebView中是否启用JavaScript。只在Android上使用，因为在iOS上默认启用了JavaScript。
- mixedContentMode(android)
  指定混合内容模式。即WebView是否应该允许安全链接（https）页面中加载非安全链接（http）的内容,
  - 'never' (默认) - WebView不允许安全链接页面中加载非安全链接的内容
  - 'always' - WebView允许安全链接页面中加载非安全链接的内容。
  - 'compatibility' - WebView会尽量和浏览器当前对待此情况的行为一致
- userAgent(android)
  为WebView设置user-agent字符串标识。这一字符串也可以在原生端用WebViewConfig来设置，但js端的设置会覆盖原生端的设置。
- allowsInlineMediaPlayback（ios）
  指定HTML5视频是在网页当前位置播放还是使用原生的全屏播放器播放。 默认值为false,视频在网页播放还需要设置webkit-playsinline
- bounces(ios)
  指定滑动到边缘后是否有回弹效果。
- decelerationRate（ios）
  指定一个浮点数，用于设置在用户停止触摸之后，此视图应以多快的速度停止滚动。也可以指定预设的字符串值，如"normal"和"fast"，
- scrollEnabled（ios）
  是否启用滚动

# 函数

- injectJavaScript
  函数接受一个字符串，该字符串将传递给WebView，并立即执行为JavaScript
- onError
  加载失败时回调
- onLoad
  完成加载时回调
- onLoadEnd
  加载成功或者失败都会回调
- onLoadStart
  开始加载的时候回调
- onMessage
  在webView内部网页中，调用window.postMessage可以触发此属性对应的函数，通过event.nativeEvent.data获取接收到的数据，实现网页和RN之间的数据传递
- renderError
  返回一个视图用来提示用户错误
- renderLoading
  返回一个加载指示器
- onShouldStartLoadWithRequest(ios)
  请求自定义处理，返回true或false表示是否要继续执行响应的请求

# 实战分析

通过上面的介绍，我们已经对组件的属性以及函数有了大致的了解，当然只有这些是不够的，接下来就该组件的使用展开分析，效果图如文章开头的GIF图。对于该组件最简单的使用如下

1.  

   <WebView

2.  

   source={{uri:'http://www.jianshu.com/u/d5b531888b2b'}}

3.  

   style={{width:'100%',height:'100%'}}

4.  

   />

指定source属性，加载网页，设置宽和高全屏，需要注意的是必须指定宽和高，否则将不显示组件，默认宽高都是0。
给WebView增加加载时的回调

1.  

   onLoad={(e) => console.log('onLoad')}

2.  

   onLoadEnd={(e) => console.log('onLoadEnd')}

3.  

   onLoadStart={(e) => console.log('onLoadStart')}

4.  

   renderError={() => {

5.  

   console.log('renderError')

6.  

   return <View><Text>renderError回调了，出现错误</Text></View>

7.  

   }}

8.  

   renderLoading={() => {

9.  

   return <View><Text>这是自定义Loading...</Text></View>

10.  

    }}

renderError可以自定义加载错误的提示信息View.当加载错误时会回调该函数，并且显示该函数返回的View。使用此方法我们可以自定义加载错误时的提示信息。
而renderLoading函数可以自定义加载提示.当我们通过WebView加载一个网页时，往往我们有需求展示出请求的url，网页的标题，以及是否可前进或者后退。在WebView组件中有一个函数onNavigationStateChange可以实现此功能，他是在加载开始和结束的时候回调的，

1.  

   //添加属性

2.  

   onNavigationStateChange={this._onNavigationStateChange}

3.  

    

4.  

   _onNavigationStateChange = (navState) => {

5.  

   console.log(navState)

6.  

   this.setState({

7.  

   backButtonEnabled: navState.canGoBack,

8.  

   forwardButtonEnabled: navState.canGoForward,

9.  

   url: navState.url,

10.  

    status: navState.title,

11.  

    loading: navState.loading,

12.  

    });

13.  

    }

当canGoBack返回值为true时，我们就可以使用this.webview.goBack();（this.webview是WebView的引用）对网页进行回退操作，同理当canGoForward为true时我们就可以使用 this.webview.goForward();对我们的网页进行跳转操作。当我们的网页url发生改变时我们可以使用 this.webview.reload();加载新的网页。

## 加载HTML

1.  

   <WebView>

2.  

   style={{width:'100%',height:'100%'}}

3.  

   source={require('./helloworld.html');}

4.  

   </WebView>

## RN和Html通信

当WebView加载html时我们可以实现html和rn之间的通信。rn向html发生数据可以通过postMessage函数实现。如下

1.  

   this.webview.postMessage('"Hello" 我是RN发送过来的数据');

2.  

   //在html中注册事件接收rn发过来的数据并显示在html中

3.  

   document.addEventListener('message', function(e) {

4.  

   messagesReceivedFromReactNative += 1;

5.  

   document.getElementsByTagName('p')[0].innerHTML =

6.  

   '从React Native接收的消息: ' + messagesReceivedFromReactNative;

7.  

   document.getElementsByTagName('p')[1].innerHTML = e.data;

8.  

   });

9.  

    

在html中我们定义了一个按钮，并添加事件向rn发送数据

1.  

   //window.postMessage向rn发送数据

2.  

   document.getElementsByTagName('button')[0].addEventListener('click', function() {

3.  

   window.postMessage('这是html发送到RN的消息');

4.  

   });

当html中调用了window.postMessage函数后，WebView的onMessage函数将会被回调，用来处理html向rn发送的数据,可以通过e.nativeEvent.data获取发送过来的数据。

1.  

   //接收HTML发出的数据

2.  

   _onMessage = (e) => {

3.  

   this.setState({

4.  

   messagesReceivedFromWebView: this.state.messagesReceivedFromWebView + 1,

5.  

   message: e.nativeEvent.data,

6.  

   })

7.  

   Alert.alert(e.nativeEvent.data)

8.  

   }

# JavaScript

在android这个需要使用 javaScriptEnabled属性来支持JavaScript，ios默认是支持的，没有此属性。在WebView中提供了函数injectJavaScript（String）,它有一个字符串参数，可以向webview中注入脚本，如下

1.  

   //脚本注入

2.  

   injectJS = () => {

3.  

   const script = 'document.write("Injected JS ")'; // eslint-disable-line quotes

4.  

   if (this.webview) {

5.  

   this.webview.injectJavaScript(script);

6.  

   }

7.  

   }

最后需要注意的一点，ScrollView中嵌套WebView时滑倒会有冲突，需要特殊处理（目前还没研究处理方法。）今天的这篇文章就介绍这么多，所介绍的实例中，只提供了核心代码，如果想查看全部代码可以访问[GitHub](https://github.com/xiehui999/helloReactNative),由于认知有限，若有错误的地方欢迎指出，共同进步，谢谢。