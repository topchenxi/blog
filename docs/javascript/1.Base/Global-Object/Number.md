# Number

## Number 定义
```javascript
// Number 对象
// Number 对象是原始数值的包装对象。
// 创建 Number 对象的语法：
// 参数 value 是要创建的 Number 对象的数值，或是要转换成数字的值。
var value = 3.1415;
var myNum = new Number(value);
var myNum = Number(value);
```

## Number 对象属性

```javascript
// MAX_VALUE	可表示的最大的数。
// MIN_VALUE	可表示的最小的数。
// NEGATIVE_INFINITY	负无穷大，溢出时返回该值。
// POSITIVE_INFINITY	正无穷大，溢出时返回该值。

console.log("最大的数: " + Number.MAX_VALUE);
console.log("最小的数: " + Number.MIN_VALUE);
console.log("负无穷大: " + Number.NEGATIVE_INFINITY);
console.log("正无穷大: " + Number.POSITIVE_INFINITY);
```

## 	Number 对象方法

```javascript
// toLocaleString	把数字转换为字符串，使用本地数字格式顺序。
// toFixed	把数字转换为字符串，结果的小数点后有指定位数的数字。
// toExponential	把对象的值转换为指数计数法。
// toPrecision	把数字格式化为指定的长度。
console.log("转换成字符串" + myNum.toLocaleString());
console.log("保留两位小数：" + myNum.toFixed(2));
console.log("指数计数法：" + myNum.toExponential());
console.log("保留两位数：" + myNum.toPrecision(2));

```
