# 编程规范

## HTML篇

标签

```html
自闭合（self-closing）标签，无需闭合 ( 例如： img input br hr 等 )；
可选的闭合标签（closing tag），需闭合 ( 例如：</li> 或 </body> )；
尽量减少标签数量；
```

Class 与 ID
```
class 应以功能或内容命名，不以表现形式命名；
class 与 id 单词字母小写，多个单词组成时，采用中划线-分隔；
使用唯一的 id 作为 Javascript hook, 同时避免创建无样式信息的 class；
```

属性顺序
```
id
class
name
data-xxx
src, for, type, href
title, alt
aria-xxx, role
```

引号
```
属性的定义，统一使用双引号。
```

嵌套
```
a 不允许嵌套 div这种约束属于语义嵌套约束，与之区别的约束还有严格嵌套约束，比如a 不允许嵌套 a。

严格嵌套约束在所有的浏览器下都不被允许；而语义嵌套约束，浏览器大多会容错处理，生成的文档树可能相互不太一样。

比如:
<li> 用于 <ul> 或 <ol> 下；
<dd>, <dt> 用于 <dl> 下；
<thead>, <tbody>, <tfoot>, <tr>, <td> 用于 <table> 下；

inline-Level 元素，仅可以包含文本或其它 inline-Level 元素;
<a>里不可以嵌套交互式元素<a>、<button>、<select>等;
<p>里不可以嵌套块级元素<div>、<h1>~<h6>、<p>、<ul>/<ol>/<li>、<dl>/<dt>/<dd>、<form>等。

```

布尔值属性
```
HTML5 规范中 disabled、checked、selected 等属性不用设置值。
<input type="text" disabled>

<input type="checkbox" value="1" checked>

<select>
  <option value="1" selected>1</option>
</select>
```

## css篇

代码组织

```
以组件为单位组织代码段；
制定一致的注释规范；
组件块和子组件块以及声明块之间使用一空行分隔，子组件块之间三空行分隔；
如果使用了多个 CSS 文件，将其按照组件而非页面的形式分拆，因为页面会被重组，而组件只会被移动
```

Class 和 ID

```
使用语义化、通用的命名方式；
使用连字符 - 作为 ID、Class 名称界定符，不要驼峰命名法和下划线；
避免选择器嵌套层级过多，尽量少于 3 级；
避免选择器和 Class、ID 叠加使用；

出于性能考量，在没有必要的情况下避免元素选择器叠加 Class、ID 使用。

元素选择器和 ID、Class 混合使用也违反关注分离原则。如果HTML标签修改了，就要再去修改 CSS 代码，不利于后期维护。
```

声明顺序
```
相关属性应为一组，推荐的样式编写顺序

Positioning
Box model
Typographic
Visual

由于定位（positioning）可以从正常的文档流中移除元素，并且还能覆盖盒模型（box model）相关的样式，因此排在首位。盒模型决定了组件的尺寸和位置，因此排在第二位。
```

引号使用
```
url() 、属性选择符、属性值使用双引号。
```
```css
@import url("//www.google.com/css/maia.css");

html {
  font-family: "open sans", arial, sans-serif;
}

.selector[type="text"] {

}
```

媒体查询（Media query）的位置
```
将媒体查询放在尽可能相关规则的附近。不要将他们打包放在一个单一样式文件中或者放在文档底部。如果你把他们分开了，将来只会被大家遗忘。

.element { ... }
.element-avatar { ... }
.element-selected { ... }

@media (max-width: 768px) {
  .element { ...}
  .element-avatar { ... }
  .element-selected { ... }
}
```

不要使用 @import
```
与 <link> 相比，@import 要慢很多，不光增加额外的请求数，还会导致不可预料的问题。

替代办法：

使用多个 元素；
通过 Sass 或 Less 类似的 CSS 预处理器将多个 CSS 文件编译为一个文件；
其他 CSS 文件合并工具；
```