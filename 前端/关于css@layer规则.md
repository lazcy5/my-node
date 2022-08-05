同一个css上下文中，有些css声明需要设置低优先级，且这种优先级不受选择器权重的影响

```css
/* 后者比前者权重更高 */
.container .some-button {}
body .container .some-button {}

body a { color: blue; }
body a:hover { color: blue; }

:any-link { color: blue; }
:any-link:hover { color: darkblue; }
```

> @layer 可以让css声明的优先级下降一整个级联级别。

##### 写在@layer 规则中的css可以把自身的优先级降到底部。

```css
/* 子组件样式 */
@layer {
  :any-link:hover { color: blue; }
}
/* 父组件样式 */
a:hover { color: red; }

/* 此时鼠标滑过链接会显示红色 */
```

##### @layer 的语法规则

```css
@layer layer-name {rules};
@layer layer-name;
@layer layer-name, layer-name, layer-name;
@layer {rules};
```

```css
@layer button {
  .container .some-button {
    height: 30px;
  }
};
@layer link {
  :any-link {
    color: blue;
  }
  :any-link:hove {
    color: darkblue;
  }
}
```

如果我们希望 xinxu 级联层的优先级大于 zhang 这个级联层的优先级，使用多名称语法设置下前后位置就可以了。

```css
@layer xinxu, zhang;
@layer zhang {
  button { padding: 10px; }
}
@layer xinxu {
  button { padding: 20px; }
}
```

##### 让整个CSS文件变成 @layer

1 @import 中使用

```css
@import './zxx.lib.css' layer(lib);
```

如果想要调整 layer(some-name) 的优先级，可以参照多名称那里的用法

```css
layer zhangxinxu, lib;
@import './zxx.lib.css' layer(lib);
@layer zhangxinxu {

}
```

##### 2 `<link >`元素引用(*)

```html
<!-- zxx-lib.css的样式属于名为 lib 的级联层 -->
<link rel="stylesheet" href="zxx-lib.css" layer="lib">

<!-- 样式引入到一个匿名级联层中 -->
<link rel="stylesheet" href="zxx-lib.css" layer>
```

注意，`<link>` 元素支持自定义的 `layer` 属性的语法目前处于[打算开发的阶段](https://github.com/whatwg/html/issues/7540)，并没有正式支持。

##### @layer 规则的嵌套

```css
@layer 甲 {
  p { color: red; }
  @layer 乙 {
    p { color: green; }
  }
}
@layer 丙 {
  p { color: orange; }
  @layer 丁 {
    p { color: blue; }
  }
}
/* 其中的优先级大小是这样的：丙 > 丙.丁 > 甲 > 甲.乙 */
```

