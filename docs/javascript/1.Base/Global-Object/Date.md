# Date

## Date 定义
```js
// Date 对象
// Date 对象用于处理日期和时间。
// 创建 Date 对象的语法：
var myDate = new Date()
```

## Date 对象方法
```javascript

myDate.getTime() 			// 返回 1970 年 1 月 1 日至今的毫秒数。

myDate.getFullYear()		// 从 Date 对象以四位数字返回年份。
myDate.getMonth()			// 从 Date 对象返回月份 (0 ~ 11)。
myDate.getDate() 			// 从 Date 对象返回一个月中的某一天 (1 ~ 31)。
myDate.getDay()				// 从 Date 对象返回一周中的某一天 (0 ~ 6)。
myDate.getHours()			// 返回 Date 对象的小时 (0 ~ 23)。
myDate.getMinutes()			// 返回 Date 对象的分钟 (0 ~ 59)。
myDate.getSeconds()			// 返回 Date 对象的秒数 (0 ~ 59)。
myDate.getMilliseconds()	// 返回 Date 对象的毫秒(0 ~ 999)。

myDate.getTimezoneOffset() 	// 返回本地时间与格林威治标准时间 (GMT) 的分钟差。

myDate.getUTCDate()			// 根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。
myDate.getUTCMonth()		// 根据世界时从 Date 对象返回月份 (0 ~ 11)。
myDate.getUTCFullYear()		// 根据世界时从 Date 对象返回四位数的年份。
myDate.getUTCDay()			// 根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。

myDate.getUTCHours() 		// 根据世界时返回 Date 对象的小时 (0 ~ 23)。
myDate.getUTCMinutes() 		// 根据世界时返回 Date 对象的分钟 (0 ~ 59)。
myDate.getUTCSeconds() 		// 根据世界时返回 Date 对象的秒钟 (0 ~ 59)。
myDate.getUTCMilliseconds() // 根据世界时返回 Date 对象的毫秒(0 ~ 999)。


myDate.toTimeString()		// 把 Date 对象的时间部分转换为字符串。
myDate.toDateString()		// 把 Date 对象的日期部分转换为字符串。
myDate.toUTCString()		// 根据世界时，把 Date 对象转换为字符串。
myDate.toLocaleString()		// 根据本地时间格式，把 Date 对象转换为字符串。
myDate.toLocaleTimeString()	// 根据本地时间格式，把 Date 对象的时间部分转换为字符串。
myDate.toLocaleDateString()	// 根据本地时间格式，把 Date 对象的日期部分转换为字符串。

myDate.UTC()				// 根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。
Date.UTC(2016, 4, 27)

// setDate()	设置 Date 对象中月的某一天 (1 ~ 31)。
// setMonth()	设置 Date 对象中月份 (0 ~ 11)。
// setFullYear()	设置 Date 对象中的年份（四位数字）。
// setYear()	请使用 setFullYear() 方法代替。
// setHours()	设置 Date 对象中的小时 (0 ~ 23)。
// setMinutes()	设置 Date 对象中的分钟 (0 ~ 59)。
// setSeconds()	设置 Date 对象中的秒钟 (0 ~ 59)。
// setMilliseconds()	设置 Date 对象中的毫秒 (0 ~ 999)。
// setTime()	以毫秒设置 Date 对象。
// setUTCDate()	根据世界时设置 Date 对象中月份的一天 (1 ~ 31)。
// setUTCMonth()	根据世界时设置 Date 对象中的月份 (0 ~ 11)。
// setUTCFullYear()	根据世界时设置 Date 对象中的年份（四位数字）。
// setUTCHours()	根据世界时设置 Date 对象中的小时 (0 ~ 23)。
// setUTCMinutes()	根据世界时设置 Date 对象中的分钟 (0 ~ 59)。
// setUTCSeconds()	根据世界时设置 Date 对象中的秒钟 (0 ~ 59)。
// setUTCMilliseconds()	根据世界时设置 Date 对象中的毫秒 (0 ~ 999)。

```