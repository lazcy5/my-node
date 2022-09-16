##### 1 函数扩展

```javascript
// 设置参数默认值
function add({host: '127.0.0.1', root, port}) {
	console.log(host, root, port)
}
// 调用方式,适用传参参数不完整
add({ host: '127.0.1.1', root: 'root', port: 3306}); // 输出 127.0.1.1 root 3306
add({ root: 'root', port: 3306 }); // 输出 127.0.0.1 root 3306
```

