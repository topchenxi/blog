# less

## 例子
```css
.clearfix {
    zoom: 1;
    &:before,
    &:after {
        display: table;

        content: '';
    }
    &:after {
        clear: both;
    }
}
```

## 变量
```css
@nice-blue: #5B83AD;
@light-blue: @nice-blue +#111;

#header {
    color: @light-blue;
}
```
编译后
```css
#header {
  color: #6c94be;
}
```

## Mixins
```css
.bordered {
    border-top: dotted 1px black;
    border-bottom: solid 2px black;
}
#menu a {
    .bordered;
}
```
编译后
```css
.bordered {
  border-top: dotted 1px black;
}
#menu a {
  border-top: dotted 1px black;
}
```

## 方法
```css
.box-shadow(@style, @c) when (iscolor(@c)) {
    -webkit-box-shadow: @style @c;
    box-shadow: @style @c;
}
.box-shadow(@style, @alpha: 50%) when (isnumber(@alpha)) {
    .box-shadow(@style, rgba(0, 0, 0, @alpha));
}
.box {
    div {
        .box-shadow(0 0 5px, 30%)
    }
}
```
编译后
```css
.box div {
  -webkit-box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  box-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
}
```

## 相关文献
[Less 中文网](http://lesscss.cn/)