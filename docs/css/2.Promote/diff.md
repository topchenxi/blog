# CSS 预处理器

## 基本语法

Less 的基本语法属于「CSS 风格」

Sass、Stylus 相比之下激进一些，利用缩进、空格和换行来减少需要输入的字符

不过区别在于 Sass、Stylus 同时也兼容「CSS 风格」代码

Less & SCSS：

```css
.box {
  display: block;
}
```

Sass：

```css
.box
  display: block
```

Stylus：

```css
.box
  display: block
```
注：后面的 Sass 代码会用被更多人接受的 SCSS 风格给出


## 嵌套语法
三者的嵌套语法都是一致的，甚至连引用父级选择器的标记 & 也相同。

区别只是 Sass 和 Stylus 可以用没有大括号的方式书写

less

```css
.a {
  &.b {
    color: red;
  }
}
```


## 变量

变量无疑为 CSS 增加了一种有效的复用方式，减少了原来在 CSS 中无法避免的重复「硬编码」

Less：
```css
@red: #c00;

strong {
  color: @red;
}
```

Sass：

```css
$red: #c00;

strong {
  color: $red;
}
```
Stylus：
```css
red = #c00

strong
  color: red
```

## import

Less 中可以在字符串中进行插值：
```css
@device: mobile;
@import "styles.@{device}.css";
```

Sass 中只能在使用 url() 表达式引入时进行变量插值：
```css
$device: mobile;
@import url(styles.#{$device}.css);
```

Stylus 中在这里插值不管用，但是可以利用其字符串拼接的功能实现：
```css
device = "mobile"
@import "styles." + device + ".css"

```

## 混入
混入（mixin）应该说是预处理器最精髓的功能之一了。

它提供了 CSS 缺失的最关键的东西：样式层面的抽象。

Less 的混入有两种方式：

1.直接在目标位置混入另一个类样式（输出已经确定，无法使用参数）；

2.定义一个不输出的样式片段（可以输入参数），在目标位置输出。

```css
.alert {
  font-weight: 700;
}

.highlight(@color: red) {
  font-size: 1.2em;
  color: @color;
}

.heads-up {
  .alert;
  .highlight(red);
}
```

编译后
```css
.alert {
  font-weight: 700;
}
.heads-up {
  font-weight: 700;
  font-size: 1.2em;
  color: red;
}
```
Sass

```css
@mixin large-text {
  font: {
    family: Arial;
    size: 20px;
    weight: bold;
  }
  color: #ff0000;
}

.page-title {
  @include large-text;
  padding: 4px;
  margin-top: 10px;
}
```

## 继承

Stylus,Scss
```css
.message
  padding: 10px
  border: 1px solid #eee

.warning
  @extend .message
  color: #e2e21e
```

less
```css
.message {
  padding: 10px;
  border: 1px solid #eee;
}

.warning {
  &:extend(.message);
  color: #e2e21e;
}
```

Sass
```css
.active {
   color: red;
}
button.active {
   @extend .active;
}
```

## 函数

三种预处理器都自带了诸如色彩处理、类型判断、数值计算等内置函数

stylus
```css
@function golden-ratio($n) {
  @return $n * 0.618;
}

.golden-box {
  width: 200px;
  height: golden-ratio(200px);
}
```

## 总结

Less 从语言特性的设计到功能的健壮程度和另外两者相比都有一些缺陷，但用 Less 可以满足大多数场景的需求。

但相比另外两者，基于 Less 开发类库会复杂得多，实现的代码会比较脏，能实现的功能也会受到 DSL 的制约。

比 Stylus 语义更清晰、比 Sass 更接近 CSS 语法，使得刚刚转用 CSS 预编译的开发者能够更平滑地进行切换。

Sass 在三者之中历史最久，也吸收了其他两者的一些优点。

从功能上来说 Sass 大而全，语义明晰但是代码很容易显得累赘。

主项目基于 Ruby 可能也是一部分人不选择它的理由（Less 开始也是基于 Ruby 开发，后来逐渐转到 less.js 项目中）。 

Sass 有一个「事实标准」库——Compass，于是对于很多开发者而言省去了选择类库的烦恼，对于提升开发效率也有不小的帮助。

Stylus 的语法非常灵活，很多语义都是根据上下文隐含的。

基于 Stylus 可以写出非常简洁的代码，但对使用团队的开发素养要求也更高，更需要有良好的开发规范或约定。

总的来说，三种预处理器百分之七八十的功能是类似的。

Less 适合帮助团队更快地上手预处理代码的开发，而 Sass 和 Stylus 的差异更在于口味。

比如有的人喜欢 jQuery 用一个 $ 做大部分的事，而另一些人觉得不一样的功能就该有明确的语义上的差别。在这里我不会做具体的推荐。当然，再次声明一下由于我个人接触 Less 开发比较多，所以可能遇到的坑也多一些，文中没有列出 Sass 和 Stylus 的问题并不代表他们没有。