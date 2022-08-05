##### RN做一个长文本折叠组件

https://blog.csdn.net/Jump_Monkey/article/details/103957500

打开虚拟小键盘

模拟器菜单I/O->keyboard

小键盘收起的代码

```

```



extraScrollHeight={-45} 解决小键盘与绝对定位布局间的空隙

```
<KeyboardAwareScrollView behavior="padding" extraScrollHeight={-45}
          resetScrollToCoords={{ x: 0, y: 0 }}
            scrollEnabled={false}>
```



```
alignSelf:'flex-start',  放在view 内部的Text宽度自适应不会占满一行
```

