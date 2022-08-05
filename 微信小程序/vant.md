#### 解决h5使用van-uploader组件上传图片调取安卓相机失效问题

```
   <van-cell title="上传图片" />
   <van-uploader
        v-model="fileList"
        :before-read="beforeRead"
        :after-read="afterRead"
        :before-delete="beforeDelete"
        :max-size="10*1024*1024"
        :max-count="3"
        upload-text="上传"
        multiple
        :capture="androidAttrs ? 'camera' : null"
        @oversize="onOversize"


// 在页面一进来时就去判断当前使用机型
const model=navigator.userAgent;
// 判断是否是安卓手机，是则是true
this.androidAttrs=model.indexOf('Android') > -1 || model.indexOf('Linux') >-1
// 总结：刚开始遇到这个问题时我也去看了好多论坛里面的各种解决方法，但是都不行。后面无意中看到了一个贴子说的是使用input上传文件然后判断后还要去删除节点，于是我就跟着一样去试一下发现vant ui不能去到封装后的节点具体属性，所以无法去处属性节点。这里要去除恶节点就是capture这个属性，ios系统不需要这个属性，而安卓系统需要这个属性才能同时调取相机和相册。所以我想了一下既然判断手机系统可行，那我为何不写一个三目运算在这个属性上，于是这样试了一下，果然可行！试了大概十几种方法终于可行了。。。真不容易呀。目前这种方式遇到一个兼容小问题就是在iphone12上调取相机拍照会闪退，调取相机没事。然后使用了oppo 华为 小米 ipone11等机型测试均无问题
```

