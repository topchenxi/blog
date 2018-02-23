# string

## string 定义
```javascript
// String 对象
// String 对象用于处理文本（字符串）。
// 创建 String 对象的语法：
var s = "Hello world!"
var str1 = new String(s);
var str2 = String(s);

// 当 String() 和运算符 new 一起作为构造函数使用时，它返回一个新创建的 String 对象，存放的是字符串 s 或 s 的字符串表示。
// 当不用 new 运算符调用 String() 时，它只把 s 转换成原始的字符串，并返回转换后的值。

// String 对象属性
var str = new String("Hello World!");
console.log(str.length);
```

## String 对象方法
```javascript
// anchor()	    创建 HTML 锚。
str.anchor()
// big()	    用大号字体显示字符串。
str.big()
// blink()	    显示闪动字符串。
str.blink()
// bold()	    使用粗体显示字符串。
str.bold()
// fontcolor()	使用指定的颜色来显示字符串。
str.fontcolor('#e50000')
// fontsize()	使用指定的尺寸来显示字符串。
// str.fontsize('14')
// italics()	使用斜体显示字符串。
str.italics()
// link()	    将字符串显示为链接。
str.link()
// small()	    使用小字号来显示字符串。
str.small()
// strike()	    使用删除线来显示字符串。
str.strike()
// sub()	    把字符串显示为下标。
str.sub()
// sup()	    把字符串显示为上标。
str.sup()
// toLocaleLowerCase()	把字符串转换为小写。
str.toLocaleLowerCase()
// toLocaleUpperCase()	把字符串转换为大写。
str.toLocaleUpperCase()
// toLowerCase()	    把字符串转换为小写。
str.toLowerCase()
// toUpperCase()	    把字符串转换为大写。
str.toUpperCase()
// fixed()				以打字机文本显示字符串。
str.fixed()
// charAt()	返回在指定位置的字符。
str.charAt(0)
// charCodeAt()	返回在指定的位置的字符的 Unicode 编码。
str.charCodeAt(0)
// concat()	连接字符串。
str.concat(new String('Tom'))
// indexOf()	检索字符串
str.indexOf('World')
// lastIndexOf()	从后向前搜索字符串。
str.lastIndexOf('Hello')
// split()	把字符串分割为字符串数组。
var str3 = "1,2,3,4,6,7";
str3.split(',')
// slice()	提取字符串的片断，并在新的字符串中返回被提取的部分。
str.slice(6, 11)
// substr()	从起始索引号提取字符串中指定数目的字符。 （不建议使用）
str.substr(6, 5)
// substring()	提取字符串中两个指定的索引号之间的字符。
str.substring(6, 11)
// replace()	替换与正则表达式匹配的子串。
// 使用 "Marry" 替换字符串中的 "Tom"：
var str4 = "Hello Tom!";
str4.replace(/Tom/, "Marry")
// search()	检索与正则表达式相匹配的值。
str.search(/world/i)
// match()	找到一个或多个正则表达式的匹配。
// 如果没有找到任何匹配的文本， match() 将返回 null。否则，它将返回一个数组
var str5 = "1 + 2 = 3";
str5.match(/\d+/g)
```

## 判断回文字符串
```js

function palindrome(str) {
    // \W匹配任何非单词字符。等价于“[^A-Za-z0-9_]”。
    var re = /[\W_]/g;
    // 将字符串变成小写字符,并干掉除字母数字外的字符
    var lowRegStr = str.toLowerCase().replace(re, '');
    // 如果字符串lowRegStr的length长度为0时，字符串即是palindrome
    if (lowRegStr.length === 0) return true;
    // 如果字符串的第一个和最后一个字符不相同，那么字符串就不是palindrome
    if (lowRegStr[0] != lowRegStr[lowRegStr.length - 1]) return false;
    //递归
    return palindrome(lowRegStr.slice(1, lowRegStr.length - 1));
}
```

## 翻转字符串
```js
// 1 反向遍历字符串
function reverseString(str) {
    var tmp = '';
    for (var i = str.length - 1; i >= 0; i--)
        tmp += str[i];
    return tmp
}

// 2 转化成array操作
function reverseString(str) {
    var arr = str.split("");
    var i = 0,
        j = arr.length - 1;
    while (i < j) {
        tmp = arr[i];
        arr[i] = arr[j];
        arr[j] = tmp;
        i++;
        j--;
    }
    return arr.join("");
}

```

## 生成指定长度随机字符串
```js
function randomString(n) {
    var str = 'abcdefghijklmnopqrstuvwxyz0123456789';
    var tmp = '';
    for (var i = 0; i < n; i++) {
        tmp += str.charAt(Math.round(Math.random() * str.length));
    }
    return tmp;
}
```

## 统计字符串中次数最多字母
```js
function findMaxDuplicateChar(str) {
    if (str.length == 1) {
        return str;
    }
    var charObj = {};
    for (var i = 0; i < str.length; i++) {
        if (!charObj[str.charAt(i)]) {
            charObj[str.charAt(i)] = 1;
        } else {
            charObj[str.charAt(i)] += 1;
        }
    }
    var maxChar = '',
        maxValue = 1;
    for (var k in charObj) {
        if (charObj[k] >= maxValue) {
            maxChar = k;
            maxValue = charObj[k];
        }
    }
    return maxChar + '：' + maxValue;
}
```