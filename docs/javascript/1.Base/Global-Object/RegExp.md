# 正则表达式

## 正则 定义
```javascript

// RegExp 对象
// RegExp 对象表示正则表达式，它是对字符串执行模式匹配的强大工具。
// 直接量语法
// /pattern/attributes
// 创建 RegExp 对象的语法:
var pattern = "[abc]";
var attributes = "g";
var myReg = new RegExp(pattern, attributes);

// 参数 pattern 是一个字符串，指定了正则表达式的模式或其他正则表达式。
// 参数 attributes 是一个可选的字符串，包含属性 "g"、"i" 和 "m"，分别用于指定全局匹配、区分大小写的匹配和多行匹配。

// 返回值
// 一个新的 RegExp 对象，具有指定的模式和标志。如果参数 pattern 是正则表达式而不是字符串，那么 RegExp() 构造函数将用与指定的 RegExp 相同的模式和标志创建一个新的 RegExp 对象。
// 如果不用 new 运算符，而将 RegExp() 作为函数调用，那么它的行为与用 new 运算符调用时一样，只是当 pattern 是正则表达式时，它只返回 pattern，而不再创建一个新的 RegExp 对象。

// 方括号用于查找某个范围内的字符:
```

## 正则 用法
```js
// [abc]	查找方括号之间的任何字符。
/[abc]/.test("abc")		// 结果:true
/[abc]/.test("defg")	// 结果:false

// [^abc]	查找任何不在方括号之间的字符。
/[^abc]/.test("abc") 	// 结果:false 
/[^abc]/.test("defg") 	// 结果:true

// [0-9]	查找任何从 0 至 9 的数字。
/[0-9]/.test("a1b2c3")	// 结果:true
/[0-9]/.test("abc")		// 结果:false

// [a-z]	查找任何从小写 a 到小写 z 的字符。
// [A-Z]	查找任何从大写 A 到大写 Z 的字符。
// [A-z]	查找任何从大写 A 到小写 z 的字符。
/[a-z]/.test("abc") // 结果:true 
/[A-Z]/.test("abc") // 结果:false 
/[A-z]/.test("abc") // 结果:true

// (red|blue|green)	查找任何指定的选项。
var reg1 = new RegExp("blue|abl1");
reg1.test("ablue") // 结果:true 
reg1.test("abl1ue") // 结果:true

// 元字符（Metacharacter）是拥有特殊含义的字符:
// .	查找单个字符，除了换行和行结束符。
var reg2 = new RegExp("h.t");
reg2.test("That's hot!")
// 结果:true (hat,hot都是)
reg2.exec("That's hot!")
// 结果:["hat", index: 1, input: "That's hot!"] 查找第一个匹配，如果使用g属性，就会指向最后一个匹配的["hot", index: 7, input: "That's hot!"]

// \w	查找单词字符。
/\w/.exec("Give 100%!")
// 结果:["G", index: 0, input: "Give 100%!"]

// \W	查找非单词字符。
/\W/.exec("Give 100%!")
// 结果:[" ", index: 4, input: "Give 100%!"]

// \d	查找数字。
/\d/.exec("Give 100%!")
// 结果:["1", index: 5, input: "Give 100%!"]

// \D	查找非数字字符。
/\D/.exec("Give 100%!")
// 结果:["G", index: 0, input: "Give 100%!"]

// \s	查找空白字符。
/\s/.exec("Give 100%!")
// 结果:[" ", index: 4, input: "Give 100%!"]

// \S	查找非空白字符。
/\S/.exec("Give 100%!")
// 结果:["G", index: 0, input: "Give 100%!"]

// \b	匹配单词边界。在单词边界匹配的位置，单词字符后面或前面不与另一个单词字符直接相邻
// 如果未找到匹配，则返回 null。
// /\bm/    匹配 "moon" 中的 'm'；
// /oo\b/   不匹配 "moon" 中的 'oo'，因为 'oo' 后面的 'n' 是一个单词字符；
// /oon\b/  匹配 "moon" 中的 'oon'，因为 'oon' 位于字符串的末端，后面没有单词字符；
// /\w\b\w/ 不匹配任何字符，因为单词字符之后绝不会同时紧跟着非单词字符和单词字符

/\bWo/.exec("Hello World")
// 结果:["Wo", index: 6, input: "Hello World"]
/\bor/.exec("Hello World")
// 结果:null

// \B	匹配非单词边界。匹配位置的上一个和下一个字符的类型是相同的:即必须同时是单词，或必须同时是非单词字符。字符串的开头和结尾处被视为非单词字符。

/\BWo/.exec("Hello World")
// 结果:null
/\Bor/.exec("Hello World")
// 结果:["or", index: 7, input: "Hello World"]l


// \n	查找换行符。
/\n/.exec("Hello World.\nLearn Javascript.")

// \f	查找换页符。
// \r	查找回车符。
// \t	查找制表符。
// \v	查找垂直制表符。

// \xxx	查找以八进制数 xxx 规定的字符。
// 八进制 127 (W)
/\127/.exec("Hello World.World is wonderful!")
// 结果:["W", index: 6, input: "Hello World.World is wonderful!"]

// \xdd	查找以十六进制数 dd 规定的字符。
// \uxxxx	查找以十六进制数 xxxx 规定的 Unicode 字符

// 量词

// n+	匹配任何包含至少一个 n 的字符串。
/o+/.exec("Hello World.World is wonderful!")
// 结果:["o", index: 4, input: "Hello World.World is wonderful!"]

// n*	匹配任何包含零个或多个 n 的字符串。
/Wo*/.exec("Hello World.World is wonderful!")
// 对 "W" 进行全局搜索，包括其后紧跟的一个或多个 "o":
// 结果:["", index: 0, input: "Hello World.World is wonderful!"]

// n?	匹配任何包含零个或一个 n 的字符串。
/10?/.exec("1, 100 or 1000?")
// 结果:["1", index: 0, input: "1, 100 or 1000?"] (1,10,10)都符合

// n{X}	匹配包含 X 个 n 的序列的字符串。
/\d{4}/.exec("100, 1000 or 10000?")
// 结果:["1000", index: 5, input: "100, 1000 or 10000?"] //查找四个数字，有两个匹配1000和10000里的1000

// n{X,Y}	匹配包含 X 或 Y 个 n 的序列的字符串。
/\d{3,4}/.exec("100, 1000 or 10000?")
// 结果:["100", index: 0, input: "100, 1000 or 10000?"] //查找三个数字或四个数字，有三个匹配100,1000和10000里的1000

// n{X,}	匹配包含至少 X 个 n 的序列的字符串。
/\d{3,}/.exec("10, 100, 1000 or 10000?")
// 结果:["100", index: 4, input: "10, 100, 1000 or 10000?"] //查找三个数字或三个以上个数字，有三个匹配100,1000和10000里的1000

// n$	匹配任何结尾为 n 的字符串。
/d!$/.exec("Hello World!")
// 结果:["d!", index: 10, input: "Hello World!"]

// ^n	匹配任何开头为 n 的字符串。
/^He/.exec("Hello World!")
// 结果:["He", index: 0, input: "Hello World!"]

// ?=n	匹配任何其后紧接指定字符串 n 的字符串。
/llo(?= Wor)/.exec("Hello World!")
// 结果:["llo", index: 2, input: "Hello World!"]

// ?!n	匹配任何其后没有紧接指定字符串 n 的字符串。
/llo(!= Wor)/.exec("Hello World!")
// 结果:null

// RegExp 对象方法
// exec	检索字符串中指定的值。返回找到的值，并确定其位置。	
/[1-9]/.exec("a1b2")
// 结果:["1", index: 1, input: "a1b2"]

// test	检索字符串中指定的值。返回 true 或 false。
/[1-9]/.test("a1b2")
// 结果:true

// 支持正则表达式的 String 对象的方法
// search	检索与正则表达式相匹配的值。
"Hello World!".search(/d!$/)
// 结果:10

// match	找到一个或多个正则表达式的匹配。
"Hello World!".match(/d!$/)
// 结果:["d!", index: 10, input: "Hello World!"]

// replace	替换与正则表达式匹配的子串。
"Hello World!".replace(/d!$/, "kkk")

// split	把字符串分割为字符串数组。
"Hello World! Football!".split(/o+/)
// 结果:["Hell", " W", "rld! F", "tball!"]
```
