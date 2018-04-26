# 注意事项

## 控制显示区域各种属性
```html
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no,viewport-fit=cover">
```
- width – `viewport` 的宽度
- height – `viewport` 的高度
- initial-scale – 初始的缩放比例
- minimum-scale – 允许用户缩放到的最小比例
- maximum-scale – 允许用户缩放到的最大比例
- user-scalable – 用户是否可以手动缩放

```html
<!-- IOS中Safari允许全屏浏览 -->
<meta content="yes" name="apple-mobile-web-app-capable">
<!-- IOS中Safari顶端状态条样式 -->
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<!-- 忽略将数字变为电话号码： -->
<!-- 一般情况下，IOS和Android系统都会默认某长度内的数字为电话号码，即使不加也是会默认显示为电话的，so，取消这个很有必要！ -->
<meta content="telephone=no" name="format-detection">
<!-- 忽略Android平台中对邮箱地址的识别 -->
<meta content="email=no" name="format-detection" />
<!-- 当网站添加到主屏幕快速启动方式，可隐藏地址栏，仅针对ios的safari -->
<meta content="yes" name="apple-mobile-web-app-capable" />
```

## 其他
关闭Input键盘默认首字母大写
```html
<input type="text" autocapitalize="off">
```
在移动端点击后会出现`暗色`的背景
```css
a, button, input, optgroup, select, textarea {
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}
```

```html
<!-- 在android或者IOS下拨打电话代码 -->
<a href="tel:15602512356">打电话给:15602512356</a>
<!-- 发短信(winphone系统无效) -->
<a href="sms:10010">发短信给: 10010</a>
<!-- 调用手机系统自带的邮件功能  -->
<a href="mailto:tugenhua@126.com">发电子邮件</a>
```

```css
body {
    font-family: "Helvetica Neue", Helvetica, sans-serif;
}
/*移动端IOS手机下清除输入框内阴影*/
input,
textarea {
    -webkit-appearance: none;
}
/*在IOS中禁止长按链接与图片弹出菜单*/
a,
img {
    -webkit-touch-callout: none;
}
```

## ios竖屏拍照上传，图片被旋转问题

上传前使用压缩工具 [lrz](https://github.com/think2011/localResizeIMG) `(推荐)`

或者
```
1.通过第三方插件exif-js获取到图片的方向
2.new一个FileReader对象，加载读取上传的图片
3.在fileReader的onload函数中，得到的图片文件用一个Image对象接收
4.在image的onload函数中，利用步骤1中获取到的方向orientation，通过canvas旋转校正，重新绘制一张新图
注意iPhone有3个拍照方向需要处理，横屏拍摄，home键在左侧，竖屏拍摄，home建上下
5.将绘制的新图转成Blob对象，添加到FormData对象中，然后进行校正后的上传操作
```

## ios：DOM元素固定一边，另一边滚动，滚动很卡的问题
```css
.class{
    /* (横向滚动用的多些)简单粗暴的办法，样式添加如下属性 */
    -webkit-overflow-scrolling: touch;
}
```

## 部分手机第三方输入法会将页面网上挤的问题
```js
// 特定需求页面，比如评论页面，输入框在顶部之类的
const interval = setInterval(function() {
    document.body.scrollTop = 0;
}, 100)
// 注意关闭页面或者销毁组件的时候记得清空定时器
clearInterval(interval);
```

## iPhoneX适配
```html
<!-- 1.viewport meta 标签增加属性viewport-fit=cover -->
<meta name="viewport" content="width=device-width, viewport-fit=cover, xxxx">
```

```css
/* 2.body元素增加样式 */
body {
  padding-bottom: constant(safe-area-inset-bottom);
  padding-bottom: env(safe-area-inset-bottom);
}
/* 3.如有fixed底部的元素，也增加上面样式 */
xxx {
  padding-bottom: constant(safe-area-inset-bottom);
  padding-bottom: env(safe-area-inset-bottom);
  background-color: #fff; 
  /* 记得添加background-color，不然会出现透明镂空的情况 */
}
```

## flex对低版本的ios和Android的支持问题
```js
// 使用postcss的autoprefixer插件，自动添加浏览器内核前缀，
// 并且增加更低浏览器版本的配置，自动添加flex老版本的属性和写法
autoprefixer({
    browsers: [
        'iOS >= 6', // 特殊处理支持低版本IOS
        'Safari >= 6', // 特殊处理支持低版本Safari
    ]
})
```

## ios 日期转换NAN的问题
```js
// 将日期字符串的格式符号替换成'/'。
'yyyy-MM-dd'.replace(/-/g, '/')
```

## 某些机型不支持video标签的poster属性，特别是安卓
```
用图片元素 <img />来代替poster
播放前显示<img />，隐藏 <video />
播放后显示<video />，隐藏 <img />
```