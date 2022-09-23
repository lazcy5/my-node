##### 1.标准盒模型和怪异盒模型

标准盒模型=width+padding(左右)+border(左右)+margin(左右)

怪异盒模型=width+margin(左右)

box-sizing:content-box时，为标准模式，也是默认模式

box-sizing:border-box时，为怪异模式

##### 2.不规则图形实现

https://coupon.codelabo.cn/?fileGuid=dpWDG6kDhy66gRVq

##### 3.表格头部首列固定实现思路

```

```

##### 3 自动填充问题

```javascript
<input readonly onfocus="this.removeAttribute('readonly');"/>   
在input框行内写这句话，可以解决用户名、密码自动填充问题

<input />   
```

##### 4 为透明图片添加阴影

```bash
# 给图片外边框增加阴影
box-shadow: 2px 4px 8px #3723a1;

# drop-shadow 的工作方式是，其遵循给给定图片的 Alpha 通道。因此阴影是基于图片的内部形状，而不是显示在图片外面。
filter: drop-shadow(2px 4px 8px #3723a1);
```

##### 5 给对应元素设置鼠标形状

```bash
# 图片
cursor: url("https://p1-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/0ac1d8cb2b1b46a384e986a7461df26a~tplv-k3u1fbpfcp-watermark.image?"), auto;

# 图标
cursor: url("data:image/svg+xml;utf8,<svg xmlns='http://www.w3.org/2000/svg'  width='48' height='48' viewport='0 0 100 100' style='fill:black;font-size:24px;'><text y='50%'>🚀</text></svg>"), auto;
```

##### 6  使用 attr() 展示 tooltip

```html
<h1>
  HTML/CSS tooltip
</h1>
<p>
  Hover <span class="tooltip" tooltip-data="Tooltip Content">Here</span> to see the tooltip.
</p>
<p>
  You can also hover <span class="tooltip" tooltip-data="This is another Tooltip Content">here</span> to see another example.
</p>

.tooltip {
  position: relative;
  border-bottom: 1px dotted black;
}

.tooltip:before {
  content: attr(tooltip-data); 
  position: absolute;
  width: 250px;
  background-color: #efba93;
  color: #fff;
  text-align: center;
  padding: 15px;
  line-height: 1.1;
  border-radius: 5px;
  z-index: 1;
  opacity: 0;
  transition: opacity .5s;
  bottom: 125%;
  left: 50%;
  margin-left: -60px;
  font-size: 0.70em;
  visibility: hidden;
}

.tooltip:after {
  content: "";
  position: absolute;
  bottom: 75%;
  left: 50%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  opacity: 0;
  transition: opacity .5s;
  border-color: #000 transparent transparent transparent;
  visibility: hidden;
}

.tooltip:hover:before, 
.tooltip:hover:after {
  opacity: 1;
  visibility: visible;
}
```

##### 7 使用 `:is()` 和 `:where()` 添加元素样式

```html
<h2 class="content-title">Header 2 <b>content title</span></h2>

:where(h2,h3,h4) > b {
  color: blue;
}

:is(h2):where(.content-title) {
  text-transform: uppercase;
}
```

##### 8 使用 first-letter 实现首字母大写

```
.content-section p:first-of-type::first-letter {
    color: #f3f3f3;
    float:  left;
    font-size: 4rem;
    line-height: 4vw;
    padding-right: 8px;
 /* border: 0.25em double; */
}
```

##### 9 谷歌浏览器自动填充输入框背景颜色问题

```css
/* 对谷歌浏览器，QQ浏览器有效，safari浏览器无效 */
input:-internal-autofill-previewed,
input:-internal-autofill-selected {
    box-shadow: inset 0 0 0 1000px rgba(0,0,0,0) !important;
    transition: background-color 5000s ease-in-out 0s !important;
}
```

##### 10 两头渐隐的线

```css
.border{
	height: 1px;
  width: 1600px;
  background: linear-gradient(243deg,#002627 0%,#00ffcd 51%,#002627 100%);
}
```

##### 11 视频背景透明

`mix-blend-mode`混合模式中有一种混合模式名为滤色，单词是`screen`，其有一个很有意思的特性表现，那就是黑色和其它元素进行混合的时候表现为透明。

```css
body {
  background: blue;
  /*
  // 图片也可以
  // background: url('./1621317824361.jpg');
  */
}
video {
    mix-blend-mode: screen;
}
```

##### 12 斜线背景

```css
.ContentWarning > summary {
  position: relative;
  list-style: none; /** 去除默认样式 **/
  user-select: none; 
  cursor: pointer;
  /** 为其添加一个斜线背景 **/
  --stripe-color: rgb(0 0 0 / 0.1);
  background-image: repeating-linear-gradient(45deg,
      transparent,
      transparent 0.5em,
      var(--stripe-color) 0.5em,
      var(--stripe-color) 1em);
}

/** 通过var变量调整悬停时的颜色样式 **/
.ContentWarning>summary: hover,
.ContentWarning>summary: focus {
  --stripe-color: rgb(150 0 0 / 0.1);
}
```

![image-20220913110457429](/Users/louxun-ui-03lv/Library/Application Support/typora-user-images/image-20220913110457429.png)

##### 13 拼色文字

```html
<svg>
  <defs>
    <clipPath id="clipPath">
        <text x="10" y="50" style="font-size: 20px;">暗黑童话</text>
    </clipPath>
  </defs>
  <g style="clip-path: url(#clipPath);">
      <rect x="0" y="0" width="60" height="90" style="fill:#000;"/>
      <rect x="60" y="0" width="60" height="90" style="fill:#cd0000;"/>
  </g>
</svg>
```

![image-20220913155952996](/Users/louxun-ui-03lv/Library/Application Support/typora-user-images/image-20220913155952996.png)

##### 14 字体显示渐变色

```html
<span class="lig-text">挺你到底</span>
<span class="lig2">24小时</span>
.lig-text {
    display: inline-block;
    position: relative;
    color: #fff;
    overflow: hidden;
    font-size: 32px;
    &::before{
      content: "";
      display: block;
      position: absolute;
      left: 0;
      top: 0;
      width: 260%;
      height: 100%;
      transform: translateX(0%);
      background-image: linear-gradient(90deg,transparent,transparent 50%,#1d1d1f 60%),linear-gradient(180deg,#ffb6ff 0%,#b344ff);
      background-image: linear-gradient(90deg,transparent 50%,#1d1d1f 60%),linear-gradient(180deg,#ffb6ff 0%,#b344ff);
      background-color: #ffb6ff;
      mix-blend-mode: darken; // 混合模式
    }
  }

.lig2 {
    color: transparent;
    -webkit-background-clip: text; //以盒子内的文字作为裁剪区域向外裁剪，文字之外的区域都将被裁剪掉。
    background-clip: text;
    background-image: linear-gradient(180deg,#ffb6ff,#b344ff);
    will-change: transform;
    padding-top: 0.5px;
    overflow: hidden;
    background-color: #ffb6ff 0%;
    font-size: 64px;
    line-height: 1.125;
    font-weight: 600;
    letter-spacing: .004em;
    //background-image: linear-gradient(180deg,#ffb6ff,#b344ff 10%,#ae38ff 33%,#ffb6ff 45%,#ffe3ff 50%,#ffb6ff 66%,#b344ff);
    background-size: 100% 300%;
    background-position: 50% 0;
    background-image: linear-gradient(90deg,transparent 50%,#1d1d1f 60%),linear-gradient(180deg,#ffb6ff 0%,#b344ff);
  }
```

##### mix-blend-mode

```
按效果来分可以分为这几类

基础混合模式  normal  利用图层透明度和不透明度来控制与下面的图层混合

降暗混合模式   darken,multiply,color-burn  减色模式，滤掉图像中高亮色，从而达到图像变暗

加亮混合模式  screen,lighten,color-dodge  加色模式，滤掉图像中暗色，从而达到图像变亮

融合混合模式  overlay,soft-light,hard-light   用于不同程度的对上、下两图层的融合

变异混合模式  difference,exclusion,hard-light 用于制作各种变异的图层混合

色彩叠加混合模式    hue,saturation,color,luminosity 根据图层的色相，饱和度等基本属性，完成图层融合 
```

