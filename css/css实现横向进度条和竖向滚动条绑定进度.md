##### 1 css横向进度条跟据竖向滚动条滚动距离显示进度

通过线性渐变实现。

假设我们的页面被包裹在 `<body>` 中，可以滚动的是整个 body，给它添加这样一个从左下到到右上角的线性渐变：

```css
body {
    background-image: linear-gradient(to right top, #ffcc00 50%, #eee 50%);
    background-repeat: no-repeat;
}
```

运用一个伪元素，把多出来的部分遮住：

```css
body::after {
    content: "";
    position: fixed;
    top: 5px;
    left: 0;
    bottom: 0;
    right: 0;
    background: #fff;
    z-index: -1;
}
```

滑到底的时候，进度条并没有到底是因为 `body` 的线性渐变高度设置了整个 body 的大小，我们调整一下渐变的高度：

```css
body {
    background-image: linear-gradient(to right top, #ffcc00 50%, #eee 50%);
    background-size: 100% calc(100% - 100vh + 5px);
    background-repeat: no-repeat;
}
```

##### 2  css inspiration (css灵感，各类神奇效果)

https://csscoco.com/inspiration/#/

https://github.com/chokcoco/iCSS

##### 3 css-doodle

 **A web component for drawing patterns with CSS** （一个通过CSS绘制图案的Web组件）。**css-doodle** 是通于[Shadow DOM V1](https://link.zhihu.com/?target=https%3A//w3c.github.io/webcomponents/spec/shadow/)和[Custom Elements V1](https://link.zhihu.com/?target=https%3A//html.spec.whatwg.org/multipage/scripting.html%23custom-elements)来构建的。

https://css-doodle.com/

##### 4 图标库

https://fontawesome.dashgame.com/