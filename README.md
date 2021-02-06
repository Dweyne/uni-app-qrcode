# uni-app-qrcode



> 本组件在weapp-qrcode-canvas-2d基础上进行再封装

<https://github.com/DoctorWei/weapp-qrcode-canvas-2d>

### 介绍

> 由于weapp-qrcode-canvas-2d是canvas绘成，在微信小程序不随页面滚动而滚动。类似`position:fixed`，所以将canvas生成image，再隐藏canvas就可解决。

#### 使用：(**必须设置宽高**)

```vue
<wx-qrcode style="width: 100%; height: 100rpx;" :imageUrl="imageUrl" :text="text"></wx-qrcode>
```

| 属性名       | 类型             | 默认值  | 说明                   |
| ------------ | ---------------- | ------- | ---------------------- |
| imageUrl     | String           |         | 二维码中间Logo的URL    |
| imageWidth   | [String, Number] | 50      | Logo的宽               |
| imageHeight  | [String, Number] | 50      | Logo的高               |
| isRound      | Boolean          | false   | 中间logo是否是圆形     |
| text         | String           |         | 二维码内容             |
| padding      | [String, Number] | 20      | 二维码与四周空白内边距 |
| paddingColor | String           | #FFFFFF | 空白内边距颜色         |
| background   | String           | #FFFFFF | 二维码背景颜色         |
| foreground   | String           | #000000 | 二维码前景色           |



