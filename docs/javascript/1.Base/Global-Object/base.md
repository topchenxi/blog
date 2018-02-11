# 全局方法

## 全局方法
```javascript
// 全局方法
// decodeURI()	解码某个编码的 URI。
// decodeURIComponent()	解码一个编码的 URI 组件。
// encodeURI()	把字符串编码为 URI。
// encodeURIComponent()	把字符串编码为 URI 组件。

var url = "http://wwww.baidu.com";

console.log(encodeURI(url));
// 结果：http://wwww.baidu.com

console.log(encodeURIComponent(url));
// 结果：http%3A%2F%2Fwwww.baidu.com

// eval()	计算 JavaScript 字符串，并把它作为脚本代码来执行。
console.log(eval(7 * 8));

// isFinite()	检查某个值是否为有穷大的数。
console.log(isFinite(1));

// isNaN()	检查某个值是否是数字。
console.log(isNaN(1));
// 结果:false
console.log(isNaN("1"));
// 结果:false
console.log(isNaN("hello"));
// 结构:true

// parseFloat()	解析一个字符串并返回一个浮点数。
console.log(parseFloat("3.1415"));

// parseInt()	解析一个字符串并返回一个整数。
console.log(parseFloat("3.0"));
// 结构:3
console.log(parseFloat("3.14"));
// 结果:3.14

// escape()	对字符串进行编码。
console.log(escape("hello"));

// unescape()	对由 escape() 编码的字符串进行解码。
console.log(unescape(escape("hello")));
```
