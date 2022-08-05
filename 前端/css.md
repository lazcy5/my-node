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

