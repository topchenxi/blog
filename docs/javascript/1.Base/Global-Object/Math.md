# Math

## Math 常量
```javascript
Math.E          // 返回算术常量 e，即自然对数的底数（约等于2.718）。
Math.LN2        // 返回 2 的自然对数（约等于0.693）。
Math.LN10       // 返回 10 的自然对数（约等于2.302）。
Math.LOG2E      // 返回以 2 为底的 e 的对数（约等于 1.414）。
Math.LOG10E     // 返回以 10 为底的 e 的对数（约等于0.434）。
Math.PI         // 返回圆周率（约等于3.14159）。
Math.SQRT1_2    // 返回 2 的平方根的倒数（约等于 0.707）。
Math.SQRT2      // 返回 2 的平方根（约等于 1.414）。
```

## Math 方法
```js
// abs(x)	返回数的绝对值。
Math.abs(-5)
// pow(x,y)	返回 x 的 y 次幂。
Math.pow(2, 3)
// sqrt(x)	返回数的平方根。
Math.sqrt(4)
// ceil(x)	对数进行上舍入。
Math.ceil(3.1415)
// 结果：
// floor(x)	对数进行下舍入。
Math.floor(3.1415)
// 结果：
// round(x)	把数四舍五入为最接近的整数。
Math.round(3.1415)
// 结果：
// random()	返回 0 ~ 1 之间的随机数。 返回指定范围的随机数(m-n之间)的公式：Math.random()*(n-m)+m
Math.random()
// "10-20：", Mathrandom() * (20 - 10) + 10, "取整后
// "取整后：" Math.floor(Math.random() * (20 - 10) + 10)
// max(x,y)	返回 x 和 y 中的最高值。
Math.max(5, 8, 9)
// min(x,y)	返回 x 和 y 中的最低值。
Math.min(5, 8, 9)
// exp(x)	返回 e 的指数。
Math.exp(1)
// log(x)	返回数的自然对数（底为e）。
Math.log(Math.E)
// sin(x)	返回数的正弦。
Math.sin(Math.PI/6)
// asin(x)	返回数的反正弦值。
Math.asin(0.5)*180/Math.PI
// cos(x)	返回数的余弦。
Math.cos(Math.PI/3)
// acos(x)	返回数的反余弦值。
Math.acos(0.5)*180/Math.PI
// tan(x)	返回角的正切。
Math.tan(Math.PI/4)
// atan(x)	以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。
Math.atan(1)*180/Math.PI
```

## 获取一定范围内的随机数
```js
function getRandomNumber(m, n) {
    return Math.random() * (n - m) + m;
}
console.log("整数随机数[20-30]:", Math.floor(getRandomNumber(20, 30)));
```