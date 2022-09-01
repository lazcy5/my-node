##### 1 文字底部横线定位居中

```css
.tab-item-active {
  position: relative;
}
.tab-item-active::after{
  position: absolute;
  content: '';
  left: 50%;
  bottom: 0;
  width: 32rpx;
  height: 4rpx;
  background: #0088ff;
  border-radius: 2rpx;
  transform: translateX(-50%);
}
```

