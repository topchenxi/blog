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

## 时间格式化

```js
Date.prototype.format = function(formatStr) {
    var str = formatStr;
    var Week = ['日', '一', '二', '三', '四', '五', '六'];
    str = str.replace(/yyyy|YYYY/, this.getFullYear());
    str = str.replace(/yy|YY/, (this.getYear() % 100) > 9 ? (this.getYear() % 100).toString() : '0' + (this.getYear() % 100));
    str = str.replace(/MM/, ('0' + (this.getMonth() + 1)).slice(-2));
    str = str.replace(/M/g, (this.getMonth() + 1));
    str = str.replace(/w|W/g, Week[this.getDay()]);
    str = str.replace(/dd|DD/, ('0' + this.getDate()).slice(-2));
    str = str.replace(/d|D/g, this.getDate());
    str = str.replace(/hh|HH/, ('0' + this.getHours()).slice(-2));
    str = str.replace(/h|H/g, this.getHours());
    str = str.replace(/mm/, ('0' + this.getMinutes()).slice(-2));
    str = str.replace(/m/g, this.getMinutes());
    str = str.replace(/ss|SS/, ('0' + this.getSeconds()).slice(-2));
    str = str.replace(/s|S/g, this.getSeconds());
    return str
}
```

```js
Date.prototype.format = function(format) {
    var o = {
        "M+": this.getMonth() + 1,
        "d+": this.getDate(),
        "h+": this.getHours(),
        "m+": this.getMinutes(),
        "s+": this.getSeconds(),
        "q+": Math.floor((this.getMonth() + 3) / 3),
        "S": this.getMilliseconds()
    };
    if (/(y+)/.test(format)) format = format.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
    for (var k in o) {
        if (new RegExp("(" + k + ")").test(format))
            format = format.replace(RegExp.$1, RegExp.$1.length == 1 ? o[k] : ("00" + o[k]).substr(("" + o[k]).length));
    }
    return format;
}
```

## n天后的时间
```js
function formatDate(n) {
    var time = new Date().getTime() + n * 1000 * 3600 * 24;
    return new Date(time);
}
```