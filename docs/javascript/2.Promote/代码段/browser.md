# 浏览器

## 判断浏览器
```javascript
window.browser = {};
//获取炉冷却信息字符串
var ua = navigator.userAgent.toLowerCase();
//浏览器信息数组，浏览器名称+版本号
// 输入结果例如：
// 谷歌浏览器
// mozilla/5.0 (windows nt 10.0; wow64) applewebkit/537.36 (khtml, like gecko) chrome/46.0.2490.86 safari/537.36
// 火狐浏览器
// mozilla/5.0 (windows nt 10.0; wow64; rv:45.0) gecko/20100101 firefox/45.0
// IE
// mozilla/5.0 (compatible; msie 9.0; windows nt 6.1; wow64; trident/5.0; slcc2; .net clr 2.0.50727; .net clr 3.5.30729; .net clr 3.0.30729; .net4.0c)
//如果存在,IE
if ((/msie ([\d.]+)/).test(ua)) {
    browser.value = ua.match(/msie ([\d.]+)/);
    browser.version = browser.value[1]; //9.0
}
//如果存在,firefox
if ((/firefox\/([\d.]+)/).test(ua)) {
    browser.value = ua.match(/firefox\/([\d.]+)/);
    browser.version = browser.value[1]; //36.0
} //如果存在,chrome
if ((/chrome\/([\d.]+)/).test(ua)) {
    browser.value = ua.match(/chrome\/([\d.]+)/);
    browser.version = browser.value[1]; //42.0.2311.135
} //如果存在,safari
if ((/version\/([\d.]+).*safari/).test(ua)) {
    browser.value = ua.match(/version\/([\d.]+).*safari/);
    browser.version = browser.value[1]; //5.1.7
}
// alert(browser.version); //输出版本号
console.log(browser.version)
```
## 判断手机浏览器类型

```js
var BrowserInfo = {
    userAgent: navigator.userAgent.toLowerCase(),
    isAndroid: Boolean(navigator.userAgent.match(/android/ig)),
    isIphone: Boolean(navigator.userAgent.match(/iphone|ipod/ig)),
    isIpad: Boolean(navigator.userAgent.match(/ipad/ig)),
    isWeixin: Boolean(navigator.userAgent.match(/MicroMessenger/ig)),
};
```

## 判断设备类型，语言
```js
var browser = {
    ver: function() {
        var u = navigator.userAgent;
        return {
            // 移动终端浏览器版本信息
            trident: u.indexOf('Trident') > -1, // IE内核
            presto: u.indexOf('Presto') > -1, // opera内核
            webKit: u.indexOf('AppleWebKit') > -1, // 苹果、谷歌内核
            gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') == -1, // 火狐内核
            mobile: !!u.match(/AppleWebKit.*Mobile.*/), // 是否为移动终端
            ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), // ios终端
            android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1, // android终端
            iPhone: u.indexOf('iPhone') > -1, // 是否为iPhone或者QQHD浏览器
            iPad: u.indexOf('iPad') > -1, // 是否iPad
            webApp: u.indexOf('Safari') == -1, // 是否web应该程序，没有头部与底部
            uc: (u.indexOf('Android') > -1 || u.indexOf('Linux') > -1) && u.indexOf('UCBrowser') > -1 //是否安卓版本uc浏览器
        };
    }(),
    language: (navigator.browserLanguage || navigator.language).toLowerCase()
}
```


## 判断IOS, 安卓

```js
var u = navigator.userAgent,
    app = navigator.appVersion;
var isAndroid = u.indexOf('Android') > -1 || u.indexOf('Linux') > -1; //android终端或者uc浏览器
var isiOS = !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/); //ios终端
```

## UserAgent 判断微信客户端
```js
// Mozilla/5.0 (iPhone; CPU iPhone OS 8_3 like Mac OS X) AppleWebKit/600.1.4 (KHTML, like Gecko) Mobile/12F70 MicroMessenger/6.1.5 NetType/WIFI
function isWechat() {
    var ua = navigator.userAgent.toLowerCase();
    return /micromessenger/i.test(ua) || /windows phone/i.test(ua);
}
```