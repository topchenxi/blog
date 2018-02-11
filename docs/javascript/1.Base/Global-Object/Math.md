# Math

## api
```javascript
// E  返回算术常量 e，即自然对数的底数（约等于2.718）。
console.log(Math.E);
// LN2	返回 2 的自然对数（约等于0.693）。
console.log(Math.LN2);
// LN10	返回 10 的自然对数（约等于2.302）。
console.log(Math.LN10);
// LOG2E	返回以 2 为底的 e 的对数（约等于 1.414）。
console.log(Math.LOG2E);
// LOG10E	返回以 10 为底的 e 的对数（约等于0.434）。
console.log(Math.LOG10E);
// PI	返回圆周率（约等于3.14159）。
console.log(Math.PI);
// SQRT1_2	返回 2 的平方根的倒数（约等于 0.707）。
console.log(Math.SQRT1_2);
// SQRT2	返回 2 的平方根（约等于 1.414）。
console.log(Math.SQRT2);


// abs(x)	返回数的绝对值。
console.log(Math.abs(-5));

// pow(x,y)	返回 x 的 y 次幂。
console.log(Math.pow(2, 3));

// sqrt(x)	返回数的平方根。
console.log(Math.sqrt(4));

// ceil(x)	对数进行上舍入。
console.log(Math.ceil(3.1415));
// 结果：4

// floor(x)	对数进行下舍入。
console.log(Math.floor(3.1415));
// 结果：3

// round(x)	把数四舍五入为最接近的整数。
console.log(Math.round(3.1415));
// 结果：3

// random()	返回 0 ~ 1 之间的随机数。 返回指定范围的随机数(m-n之间)的公式：Math.random()*(n-m)+m
console.log(Math.random());
console.log("10-20：", Math.random() * (20 - 10) + 10, "取整后：", Math.floor(Math.random() * (20 - 10) + 10));

// max(x,y)	返回 x 和 y 中的最高值。
console.log("max(5,8,9):", Math.max(5, 8, 9));

// min(x,y)	返回 x 和 y 中的最低值。
console.log("min(5,8,9):", Math.min(5, 8, 9));

// exp(x)	返回 e 的指数。
console.log(Math.exp(1));

// log(x)	返回数的自然对数（底为e）。
console.log(Math.log(Math.E));

// sin(x)	返回数的正弦。
console.log(Math.sin(Math.PI/6));

// asin(x)	返回数的反正弦值。
console.log(Math.asin(0.5)*180/Math.PI);

// cos(x)	返回数的余弦。
console.log(Math.cos(Math.PI/3));

// acos(x)	返回数的反余弦值。
console.log(Math.acos(0.5)*180/Math.PI);

// tan(x)	返回角的正切。
console.log(Math.tan(Math.PI/4));

// atan(x)	以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。
console.log(Math.atan(1)*180/Math.PI);

```
