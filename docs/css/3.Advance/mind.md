# 注意事项

## 控制显示区域各种属性
```html
<meta name="viewport" content="width=device-width,initial-scale=1.0,minimum-scale=1.0,maximum-scale=1.0,user-scalable=no,viewport-fit=cover">
```
- width–viewport的宽度
- height–viewport的高度
- initial-scale–初始的缩放比例
- minimum-scale–允许用户缩放到的最小比例
- maximum-scale–允许用户缩放到的最大比例
- user-scalable–用户是否可以手动缩放

```html
<!-- IOS中Safari允许全屏浏览 -->
<meta content="yes" name="apple-mobile-web-app-capable">
<!-- IOS中Safari顶端状态条样式 -->
<meta content="black" name="apple-mobile-web-app-status-bar-style">
<!-- 忽略将数字变为电话号码： -->
<!-- 一般情况下，IOS和Android系统都会默认某长度内的数字为电话号码，即使不加也是会默认显示为电话的，so，取消这个很有必要！ -->
<meta content="telephone=no" name="format-detection">
```