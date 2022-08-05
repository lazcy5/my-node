##### 1. 头部导航需要根据各个小程序的配置方式设置才能隐藏

```javascript
"pages": [
		{
			"path": "pages/index/index",
			"style": {
				"navigationBarTitleText": "首页", 
				"app-plus": {
					"titleNView": false //禁用原生导航栏
				},
				"mp-weixin": {
					"navigationStyle": "custom"
				},
				"mp-qq": {
					"navigationStyle": "custom"
				},
        ...
			}
		}
  }
```

##### 2.  .webp格式的图片

相对路径的.webp格式图片，小程序没显示，需注意。

##### 3.    对应小程序开发者工具上传代码注意检查调试基础库版本