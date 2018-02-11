# Date

## Date API
```javascript

	// Date 对象
	// Date 对象用于处理日期和时间。
	// 创建 Date 对象的语法：
	var myDate = new Date();

	// 	Date 对象方法
	// getFullYear()	从 Date 对象以四位数字返回年份。
	// getMonth()	从 Date 对象返回月份 (0 ~ 11)。
	// getDate()	从 Date 对象返回一个月中的某一天 (1 ~ 31)。
	console.log(myDate.getFullYear() + "年" + (myDate.getMonth() + 1) + "月" + myDate.getDate() + "号");

	// getDay()	从 Date 对象返回一周中的某一天 (0 ~ 6)。
	console.log("星期" + myDate.getDay());


	// getHours()	返回 Date 对象的小时 (0 ~ 23)。
	// getMinutes()	返回 Date 对象的分钟 (0 ~ 59)。
	// getSeconds()	返回 Date 对象的秒数 (0 ~ 59)。
	// getMilliseconds()	返回 Date 对象的毫秒(0 ~ 999)。
	console.log(myDate.getHours() + "时" + myDate.getMinutes() + "分" + myDate.getSeconds() + "秒" + myDate.getMilliseconds() + "毫秒");

	// getTime()	返回 1970 年 1 月 1 日至今的毫秒数。
	console.log(myDate.getTime());

	// getTimezoneOffset()	返回本地时间与格林威治标准时间 (GMT) 的分钟差。
	console.log(myDate.getTimezoneOffset());

	console.log("世界时：")
	// getUTCDate()	根据世界时从 Date 对象返回月中的一天 (1 ~ 31)。
	// getUTCMonth()	根据世界时从 Date 对象返回月份 (0 ~ 11)。
	// getUTCFullYear()	根据世界时从 Date 对象返回四位数的年份。
	console.log(myDate.getUTCFullYear() + "年" + (myDate.getUTCMonth() + 1) + "月" + myDate.getUTCDate() + "号");

	// getUTCDay()	根据世界时从 Date 对象返回周中的一天 (0 ~ 6)。
	console.log("星期" + myDate.getUTCDay());

	// getUTCHours()	根据世界时返回 Date 对象的小时 (0 ~ 23)。
	// getUTCMinutes()	根据世界时返回 Date 对象的分钟 (0 ~ 59)。
	// getUTCSeconds()	根据世界时返回 Date 对象的秒钟 (0 ~ 59)。
	// getUTCMilliseconds()	根据世界时返回 Date 对象的毫秒(0 ~ 999)。
	console.log(myDate.getUTCHours() + "时" + myDate.getUTCMinutes() + "分" + myDate.getUTCSeconds() + "秒" + myDate.getUTCMilliseconds() + "毫秒");


	// toTimeString()	把 Date 对象的时间部分转换为字符串。
	console.log("时间" + myDate.toTimeString());

	// toDateString()	把 Date 对象的日期部分转换为字符串。
	console.log("日期" + myDate.toDateString());

	// toUTCString()	根据世界时，把 Date 对象转换为字符串。
	console.log(myDate.toUTCString());

	// toLocaleString()	根据本地时间格式，把 Date 对象转换为字符串。
	console.log(myDate.toLocaleString());

	// toLocaleTimeString()	根据本地时间格式，把 Date 对象的时间部分转换为字符串。
	console.log("时间" + myDate.toLocaleTimeString());

	// toLocaleDateString()	根据本地时间格式，把 Date 对象的日期部分转换为字符串。
	console.log("日期" + myDate.toLocaleDateString());

	// UTC()	根据世界时返回 1970 年 1 月 1 日 到指定日期的毫秒数。
	console.log(Date.UTC(2016, 4, 27));

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