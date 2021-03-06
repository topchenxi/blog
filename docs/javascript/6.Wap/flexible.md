# flexible

## 移动端适配方案 flexible.js

```html
<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, minimum-scale=1, user-scalable=no">
```
```js
// 加载阿里CDN的文件
<script src="http://g.tbcdn.cn/mtb/lib-flexible/0.3.4/??flexible_css.js,flexible.js"></script>
```

分别引入css和js模块


## css模块
```css
@charset 'utf-8';
html {
    overflow-y: scroll;

    color: #000;
    background: #fff;

    -webkit-text-size-adjust: 100%;
    -ms-text-size-adjust: 100%;
}

html * {
    outline: 0;

    -webkit-text-size-adjust: none;
    -webkit-tap-highlight-color: rgba(0, 0, 0, 0);
}

html,
body {
    font-family: sans-serif;
}

body,
div,
dl,
dt,
dd,
ul,
ol,
li,
h1,
h2,
h3,
h4,
h5,
h6,
pre,
code,
form,
fieldset,
legend,
input,
textarea,
p,
blockquote,
th,
td,
hr,
button,
article,
aside,
details,
figcaption,
figure,
footer,
header,
hgroup,
menu,
nav,
section {
    margin: 0;
    padding: 0;
}

input,
select,
textarea {
    font-size: 100%;
}

table {
    border-spacing: 0;
    ;
    border-collapse: collapse;
}

fieldset,
img {
    border: 0;
}

abbr,
acronym {
    font-variant: normal;
    ;

    border: 0;
}

del {
    text-decoration: line-through;
}

address,
caption,
cite,
code,
dfn,
em,
th,
var {
    font-weight: 500;
    ;
    font-style: normal;
}

ol,
ul {
    list-style: none;
}

caption,
th {
    text-align: left;
}

h1,
h2,
h3,
h4,
h5,
h6 {
    font-size: 100%;
    font-weight: 500;
}

q:before,
q:after {
    content: '';
}

sub,
sup {
    font-size: 75%;
    line-height: 0;

    position: relative;

    vertical-align: baseline;
}

sup {
    top: -.5em;
}

sub {
    bottom: -.25em;
}

a:hover {
    text-decoration: underline;
}

ins,
a {
    text-decoration: none;
}
```

功能是重置页面样式

## js模块
```js
;(function(win, lib) {
    var doc = win.document;
    var docEl = doc.documentElement;
    var metaEl = doc.querySelector('meta[name="viewport"]');
    var flexibleEl = doc.querySelector('meta[name="flexible"]');
    var dpr = 0;
    var scale = 0;
    var tid;
    var flexible = lib.flexible || (lib.flexible = {});

    if (metaEl) {
        console.warn('将根据已有的meta标签来设置缩放比例');
        var match = metaEl.getAttribute('content').match(/initial\-scale=([\d\.]+)/);
        if (match) {
            scale = parseFloat(match[1]);
            dpr = parseInt(1 / scale);
        }
    } else if (flexibleEl) {
        var content = flexibleEl.getAttribute('content');
        if (content) {
            var initialDpr = content.match(/initial\-dpr=([\d\.]+)/);
            var maximumDpr = content.match(/maximum\-dpr=([\d\.]+)/);
            if (initialDpr) {
                dpr = parseFloat(initialDpr[1]);
                scale = parseFloat((1 / dpr).toFixed(2));
            }
            if (maximumDpr) {
                dpr = parseFloat(maximumDpr[1]);
                scale = parseFloat((1 / dpr).toFixed(2));
            }
        }
    }
    if (!dpr && !scale) {
        var isAndroid = win.navigator.appVersion.match(/android/gi);
        var isIPhone = win.navigator.appVersion.match(/iphone/gi);
        var devicePixelRatio = win.devicePixelRatio;
        if (isIPhone) {
            // iOS下，对于2和3的屏，用2倍的方案，其余的用1倍方案
            if (devicePixelRatio >= 3 && (!dpr || dpr >= 3)) {
                dpr = 3;
            } else if (devicePixelRatio >= 2 && (!dpr || dpr >= 2)) {
                dpr = 2;
            } else {
                dpr = 1;
            }
        } else {
            // 其他设备下，仍旧使用1倍的方案
            dpr = 1;
        }
        scale = 1 / dpr;
    }
    docEl.setAttribute('data-dpr', dpr);
    if (!metaEl) {
        metaEl = doc.createElement('meta');
        metaEl.setAttribute('name', 'viewport');
        metaEl.setAttribute('content', 'initial-scale=' + scale + ', maximum-scale=' + scale + ', minimum-scale=' + scale + ', user-scalable=no');
        if (docEl.firstElementChild) {
            docEl.firstElementChild.appendChild(metaEl);
        } else {
            var wrap = doc.createElement('div');
            wrap.appendChild(metaEl);
            doc.write(wrap.innerHTML);
        }
    }

    function refreshRem() {
        var width = docEl.getBoundingClientRect().width;
        if (width / dpr > 540) {
            width = 540 * dpr;
        }
        var rem = width / 10;
        docEl.style.fontSize = rem + 'px';
        flexible.rem = win.rem = rem;
    }
    win.addEventListener('resize', function() {
        clearTimeout(tid);
        tid = setTimeout(refreshRem, 300);
    }, false);
    win.addEventListener('pageshow', function(e) {
        if (e.persisted) {
            clearTimeout(tid);
            tid = setTimeout(refreshRem, 300);
        }
    }, false);
    if (doc.readyState === 'complete') {
        doc.body.style.fontSize = 12 * dpr + 'px';
    } else {
        doc.addEventListener('DOMContentLoaded', function(e) {
            doc.body.style.fontSize = 12 * dpr + 'px';
        }, false);
    }

    refreshRem();
    flexible.dpr = win.dpr = dpr;
    flexible.refreshRem = refreshRem;
    flexible.rem2px = function(d) {
        var val = parseFloat(d) * this.rem;
        if (typeof d === 'string' && d.match(/rem$/)) {
            val += 'px';
        }
        return val;
    }
    flexible.px2rem = function(d) {
        var val = parseFloat(d) / this.rem;
        if (typeof d === 'string' && d.match(/px$/)) {
            val += 'rem';
        }
        return val;
    }
})(window, window['lib'] || (window['lib'] = {}));
```

## 解释
flexible.js 做了下面三件事：

1. 动态改写标签
2. 给`<html>`元素添加`data-dpr`属性，并且动态改写`data-dpr`的值
3. 给`<html>`元素添加`font-size`属性，并且动态改写`font-size`的值

## css用法

以 750px  的移动端设计稿

flexible 会将视觉稿分成`100份`（主要为了以后能更好的兼容`vh`和`vw`），而每一份被称为一个单位`a`。同时`1rem`单位被认定为`10a`

```
1a   = 7.5px
1rem = 75px 
```

只需要记住 `1rem` = `75px` 就好

scss
```scss
@function px2rem($px){
	@return $px/75 + rem;
}
```

less(需引入less-plugin-functions)
```less
.function{
	.px2rem(@px){
		return : unit(@px/75 , rem);
	}
}
```

stylus
```stylus
px2rem(px)
  return unit(px * 320 / designWidth / 20, 'rem')
```

## 参考文献

[lib-flexible](https://github.com/amfe/lib-flexible)
