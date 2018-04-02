# scss

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
$highlight-color: #F90;
.selected {
  border: 1px solid $highlight-color;
}
```
编译后
```css
.selected {
    border: 1px solid #F90;
}
```

## Mixins
```css
@mixin rounded-corners {
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    border-radius: 5px;
}

.notice {
    @include rounded-corners;
}
```
编译后
```css
.notice {
    -webkit-border-radius: 5px;
    -moz-border-radius: 5px;
    border-radius: 5px;
}
```

## extend 
```css
.error {
    border: 1px solid red;
    background-color: #fdd;
}
.seriousError {
    color: #fff;
    @extend .error;
}
```
编译后
```css
.error,
.seriousError {
    border: 1px solid red;
    background-color: #fdd;
}
.seriousError {
    color: #fff;
}
```

## 相关文献
[Sass中文网](https://www.sass.hk/)