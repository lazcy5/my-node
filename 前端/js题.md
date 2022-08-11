



##### 1.函数防抖

一个函数连续触发，只执行最后一次

```javascript
// fn是你要调用的函数，delay是防抖的时间
function debounce(fn, delay) {
  // timer是一个定时器
  let timer = null;
  // 返回一个闭包函数，用闭包保存timer确保其不会销毁，重复点击会清理上一次的定时器
  return function () {
    // 保存事件参数，防止fn函数需要事件参数里的数据
    let arg = arguments;
    // 调用一次就清除上一次的定时器
    clearTimeout(timer);
    // 开启这一次的定时器
    timer = setTimeout(() => {
      // 若不改变this指向，则会指向fn定义环境
      fn.apply(this, arg);
    }, delay)
  }
}

```

##### 2.函数节流

限制一个函数在一段时间内只能执行一次

```javascript
// 方法一：时间戳
function throttle(fn, delay = 1000) {
  // 记录第一次的调用时间
  var prev = null;
  console.log(prev);
  // 返回闭包函数
  return function () {
    // 保存事件参数
    var args = arguments;
    // 记录现在调用的时间
    var now = Date.now();
    // console.log(now);
    // 如果间隔时间大于等于设置的节流时间
    if (now - prev >= delay) {
      // 执行函数
      fn.apply(this, args);
      // 将现在的时间设置为上一次执行时间
      prev = now;
    }
  }
}
// 方法二：定时器
function throttle(fn, delay) {
  // 重置定时器
  let timer = null;
  // 返回闭包函数
  return function () {
    // 记录事件参数
    let args = arguments;
    // 如果定时器为空
    if (!timer) {
      // 开启定时器
      timer = setTimeout(() => {
        // 执行函数
        fn.apply(this, args);
        // 函数执行完毕后重置定时器
        timer = null;
      }, delay);
    }
  }
}
// 方法三：时间戳 & 定时器
function throttle(fn, delay) {
  // 初始化定时器
  let timer = null;
  // 上一次调用时间
  let prev = null;
  // 返回闭包函数
  return function () {
    // 现在触发事件时间
    let now = Date.now();
    // 触发间隔是否大于delay
    let remaining = delay - (now - prev);
    // 保存事件参数
    const args = arguments;
    // 清除定时器
    clearTimeout(timer);
    // 如果间隔时间满足delay
    if (remaining <= 0) {
      // 调用fn，并且将现在的时间设置为上一次执行时间
      fn.apply(this, args);
      prev = Date.now();
    } else {
      // 否则，过了剩余时间执行最后一次fn
      timer = setTimeout(() => {
        fn.apply(this, args)
      }, delay);
    }
  }
}

```

##### 3.深拷贝

```javascript
function deepClone(obj, cache = new WeakMap()) {
  if (typeof obj !== 'object') return obj // 普通类型，直接返回
  if (obj === null) return obj
  if (cache.get(obj)) return cache.get(obj) // 防止循环引用，程序进入死循环
  if (obj instanceof Date) return new Date(obj)
  if (obj instanceof RegExp) return new RegExp(obj)
  
  // 找到所属原型上的constructor，所属原型上的constructor指向当前对象的构造函数
  let cloneObj = new obj.constructor()
  cache.set(obj, cloneObj) // 缓存拷贝的对象，用于处理循环引用的情况
  for (let key in obj) {
    if (obj.hasOwnProperty(key)) {
      cloneObj[key] = deepClone(obj[key], cache) // 递归拷贝
    }
  }
  return cloneObj
}

// 测试
const obj = { name: 'Jack', address: { x: 100, y: 200 } }
obj.a = obj // 循环引用
const newObj = deepClone(obj)
console.log(newObj.address === obj.address) // false

```

##### 4.ajax和axios、fetch

**ajax**:最早出现的发送后端请求技术，核心是使用XMLHttpRequest对象。

多个请求如果有先后顺序会出现回调地狱。

增加了对JSONP的支持。

```javascript
$.ajax({
   type: 'POST',
   url: url,
   data: data,
   dataType: dataType,
   success: function () {},
   error: function () {}
});
```

**Axios**:一个基于Promise用于刘安拉取和nodejs的HTTP客户端，本质是也是对原生XMLHttpRequest的封装。

特点：

1.从浏览器中创建 XMLHttpRequest
 2.支持 Promise API
 3.客户端支持防止CSRF
 4.提供了一些并发请求的接口（重要，方便了很多的操作）
 5.从 node.js 创建 http 请求
 6.拦截请求和响应
 7.转换请求和响应数据
 8.取消请求
 9.自动转换JSON数据

```javascript
axios({
    method: 'post',
    url: '/user/12345',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
})
.then(function (response) {
    console.log(response);
})
.catch(function (error) {
    console.log(error);
});
```

**fetch**:fetch号称是AJAX的替代品，是在ES6出现的，使用了ES6中的promise对象。Fetch是基于promise设计的。Fetch的代码结构比起ajax简单多了，参数有点像jQuery ajax。但是，一定记住**fetch不是ajax的进一步封装，而是原生js，没有使用XMLHttpRequest对象**。
 fetch的优点：
 1.符合关注分离，没有将输入、输出和用事件来跟踪的状态混杂在一个对象里
 2.更好更方便的写法

```
优势
1.  语法简洁，更加语义化
2.  基于标准 Promise 实现，支持 async/await
3.  同构方便，使用 [isomorphic-fetch](https://github.com/matthew-andrews/isomorphic-fetch)
4.更加底层，提供的API丰富（request, response）
5.脱离了XHR，是ES规范里新的实现方式

不足
1）fetch只对网络请求报错，对400，500都当做成功的请求，服务器返回 400，500 错误码时并不会 reject，只有网络错误这些导致请求不能完成时，fetch 才会被 reject。
2）fetch默认不会带cookie，需要添加配置项： fetch(url, {credentials: 'include'})
3）fetch不支持abort，不支持超时控制，使用setTimeout及Promise.reject的实现的超时控制并不能阻止请求过程继续在后台运行，造成了流量的浪费
4）fetch没有办法原生监测请求的进度，而XHR可以数据扁平化
```

##### 4 数据扁平化

```javascript
let flatArr = [
  {id: 1, title: "解忧杂货铺1", parent_id: 0},
  {id: 2, title: '解忧杂货铺2', parent_id: 0},
  {id: 3, title: '解忧杂货铺2-1', parent_id: 2},
  {id: 4, title: '解忧杂货铺3-1', parent_id: 3},
  {id: 5, title: '解忧杂货铺4-1', parent_id: 4},
  {id: 6, title: '解忧杂货铺2-2', parent_id: 2},
]

function convert(list) {
  const res = [];
  const map = list.reduce((res, v) => (res[v.id] = v, res), {});
  console.log(map)
  for (const item of list) {
    if (item.parent_id === 0) {
      res.push(item);
      continue;
    }
    if (item.parent_id in map) {
      const parent = map[item.parent_id];
      parent.children = parent.children || [];
      parent.children.push(item);
    }
  }
  return res;
}
let returnTree = convert(flatArr);
console.log(returnTree);
```

![image-20220617141758660](/Users/louxun-ui-03lv/Library/Application Support/typora-user-images/image-20220617141758660.png)



##### 5 100个人围成一圈，每个人的编号分别是1,2…100,从编号为1的人开始从1数到m时该人退出圈，下一个人继续从1数到m，然后退出，直到剩余的人小于m，1＜m＜100，请问打印剩余人的编号从小到大排序。

例如输入M=3时，输出为：“58,91”，输入M=4时，输出为： “34,45,97”

```javascript
let a = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17, 18, 19, 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37, 38, 39, 40, 41, 42, 43, 44, 45, 46, 47, 48, 49, 50, 51, 52, 53, 54, 55, 56, 57, 58, 59, 60, 61, 62, 63, 64, 65, 66, 67, 68, 69, 70, 71, 72, 73, 74, 75, 76, 77, 78, 79, 80, 81, 82, 83, 84, 85, 86, 87, 88, 89, 90, 91, 92, 93, 94, 95, 96, 97, 98, 99, 100]
			let b = 3
			let cc = []
			function fun(aa,bb){
				for(let i=aa.length;i>=bb;i--){
					cc=aa.slice(bb)
        	console.log(cc, 'cc========')
					aa.splice(bb-1)
					aa=[...cc,...aa]
				}
        console.log(aa, 'aa========')
				return aa
			}
			let ee = fun(a, b)
			console.log(ee);//58,91
```

原型链例子

![image-20220811101326671](/Users/louxun-ui-03lv/Documents/workerspace/markdown/my-node/image-20220811101326671.png)
