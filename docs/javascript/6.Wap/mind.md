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