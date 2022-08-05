###### 深拷贝：在堆内存中重新开辟一个存储空间，完全克隆一个一模一样的对象 浅拷贝：不在堆内存中重新开辟空间，只复制栈内存中的引用地址。本质上两个对象（数组）依然指向同一块存储空间

#### 深拷贝

##### 1. 递归拷贝-------推荐使用

```javascript
const copyObj = (0bj = {}) => {
  let newobj = null;
  // 判断是否为对象
  if(typeof (obj) == 'object' && obj != null) {
    newobj = obj instanceof Array ? [] : {};
    for (var i in obj) {
      newobj[i] = copyObj(obj[i])
    }
  } else newobj = obj;
  return newobj;
}
```

###### 完整的深拷贝递归

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

##### 2.  JSON.stringfy()

对象中有undefined类型或者function类型的元素时，深拷贝后的对象会丢失该元素

对象中有时间类型元素时，时间类型会转为字符串，无法调用时间相关的函数如geiTime()

当对象中有NaN、Infinity和-Infinity这三种值的时候 --- 会变成null

```javascript
const obj = {
	date: new Date()
}
typeof obj.date === 'object' // true
const objCopy = JSON.parse(JSON.stringfy(obj));
typeof objCopy.date === string; // true


const obj1 = {
	undef: undefined,
  fun: () => { console.log('123') }
}
const copy1 = JSON.parse(JSON.stringfy(obj1))
console.log(copy1, 'copy1') // 输出 {}copy1

const obj2 = {
	nan: NaN,
  infinityMax:1.7976931348623157E+10308,
  infinityMin:-1.7976931348623157E+10308,
}
const copy2 = JSON.parse(JSON.stringfy(obj2))
console.log(copy2, 'copy2') // 输出 { nan: null, infinityMax: null, infinityMin: null}
```

##### 3. 第三方库loadash的clone方法

##### 4.  JQuery的extend()方法

```javascript
const obj = {
	aa: 1
}
const newObj = $.extend(true, {}, obj);
```

#### 浅拷贝

##### 1 Object.assign()

```javascript
const obj = {
	aa: 1
}
const newObj = Object.assign({}, obj);
```

##### 2 slice

```javascript
const fxArr = ['one', 'two', 'three'];
const fxArrs = fxArr.slice(0);
fxArrs[1] = 'love';
console.log(fxArr); // 输出 'one', 'two', 'three'
console.log(fxArrs); // 输出 'one', 'love', 'three'
```

##### 2 concat

```javascript
const fxArr = ['one', 'two', 'three'];
const fxArrs = [...fxArr];
fxArrs[1] = 'love';
console.log(fxArr); // 输出 'one', 'two', 'three'
console.log(fxArrs); // 输出 'one', 'love', 'three'
```

##### 2 拓展运算符

```javascript
const fxArr = ['one', 'two', 'three'];
const fxArrs = [...fxArr];
fxArrs[1] = 'love';
console.log(fxArr); // 输出 'one', 'two', 'three'
console.log(fxArrs); // 输出 'one', 'love', 'three'
```

