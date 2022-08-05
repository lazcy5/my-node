### 路由

1. ##### 路由的跳转

```javascript
import { NavigationActions, NavigationActions, StackActions } from 'react-navigation';

<Button titile="创建一个新页面" onPress={()=> this.props.navigation.push('ChangePassword')} />

<Button titile="加载已有页面或创建一个新页面" onPress={()=> this.props.navigation.navigate('ChangePassword')} />

<Button titile="新页面替换当前页面" onPress={()=> this.props.navigation.replace('ChangePassword')} />

<Button titile="返回上一个页面" onPress={()=> this.props.navigation.goBack()} />

<Button titile="返回第一个页面" onPress={()=> this.props.navigation.popToTop()} />

<Button titile="在路由堆栈内返回N层" onPress={()=> this.props.navigation.pop(n)} />

<Button titile="重置路由堆栈并初始化到指定页面" onPress={()=> {
  this.props.navigation.reset([NavigationActions.navigate({ routeName: 'Home' })], 0)
  
  // 扩展： dispatch执行
  //  const resetAction = StackActions.reset({
  //  index: 0,
  //  actions: [NavigationActions.navigate({ routeName: 'Home' })],
  //  })
  // this.props.navigation.dispatch(resetAction);
}} />
```

2. ##### 路由方法

```javascript
this,props.navigation.addListener(()=> {
  // 订阅导航生命周期的更新
})

this,props.navigation.isFocused((bool)=> {
  // 函数返回true/false  屏幕焦点
})

this,props.navigation.setParams(()=> {
  // 对路由参数进行更改
  title: 'xxx',
  save: this.save.bind(this),
})

// 获取参数
this.props.navigation.state.params.title;
// 获取参数title, 获取失败取默认值profile
this.props.navigation.getParam('title', 'profile');
```

