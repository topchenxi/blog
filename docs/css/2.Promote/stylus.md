# stylus

## 例子
```css
.clearfix
	zoom:1
	&:before
	&:after
		dispaly:table
		content:''
	&:after
		clear:both
```
## 变量
```css
/* 变量 */
font-size = 14px
/* 表达式列 */
font = font-size "Lucida Grande", Arial

```
编译后
```css
body {
  font: 14px "Lucida Grande", Arial sans-serif;
}
```

## Mixins
```css
border-radius(n)
  -webkit-border-radius n
  -moz-border-radius n
  border-radius n

form input[type=button]
  border-radius(5px)
```
编译后
```css
form input[type=button] {
  -webkit-border-radius: 5px;
  -moz-border-radius: 5px;
  border-radius: 5px;
}
```

## 方法
```css
add(a, b)
  a + b
  
body 
  padding add(10px, 5)
```
编译后
```css
body {
  padding: 15px;
}
```

## 相关文献

[stylus中文文档 - 张鑫旭](http://www.zhangxinxu.com/jq/stylus/)