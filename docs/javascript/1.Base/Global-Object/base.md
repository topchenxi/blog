# 全局方法

## 全局方法
```javascript
// 全局方法
// decodeURI()	解码某个编码的 URI。
// decodeURIComponent()	解码一个编码的 URI 组件。
// encodeURI()	把字符串编码为 URI。
// encodeURIComponent()	把字符串编码为 URI 组件。

var url = "http://wwww.baidu.com";

encodeURI(url) // 结果：http://wwww.baidu.com
encodeURIComponent(url) // 结果：http%3A%2F%2Fwwww.baidu.com

eval(7 * 8) // 计算 JavaScript 字符串，并把它作为脚本代码来执行。


isFinite(1) // 检查某个值是否为有穷大的数。

// isNaN()	检查某个值是否是数字
isNaN(1) // 结果:false
isNaN("1") // 结果:false
isNaN("hello") // 结果:true



parseFloat("3.1415") // parseFloat()	解析一个字符串并返回一个浮点数。

parseFloat("3.0") // parseInt()	解析一个字符串并返回一个整数。
// 结构:3
parseFloat("3.14")
// 结果:3.14

escape("hello") // escape()	对字符串进行编码。

unescape(escape("hello")) // unescape()	对由 escape() 编码的字符串进行解码。
```

## 获取链接参数
```js
function getUrlParam(name) {
    // 构造一个含有目标参数的正则表达式对象  
    var reg = new RegExp("(^|&)" + name + "=([^&]*)(&|$)");
    // 匹配目标参数  
    var r = window.location.search.substr(1).match(reg);
    if (r != null) return unescape(r[2]);
    //返回参数值
    return null;
}
```

```js
const getUrlParameters = url => url.match(/([^?=&]+)(=([^&]*))/g).reduce(
    (a, v) => (
        a[v.slice(0, v.indexOf('='))] = v.slice(v.indexOf('=') + 1), a
    ), {}
);
// console.log(getUrlParameters('http://baidu.com?a=1&b=2&c=3')) 
// {a: "1", b: "2", c: "3"}
```

## 验证数字
```js
const validateNumber = n => !isNaN(parseFloat(n)) && isFinite(n) && Number(n) == n;
```