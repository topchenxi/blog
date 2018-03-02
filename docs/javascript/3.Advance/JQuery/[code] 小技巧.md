# jQuery 代码段

## 禁止右键点击
```js
$(document).ready(function() {
    $(document).bind("contextmenu", function(e) {
        return false;
    });
});

```
##  隐藏搜索文本框文字
```js
$(document).ready(function() {
    $("input.text1").val("Enter your search text here");
    textFill($('input.text1'));
});

function textFill(input) {
    var originalvalue = input.val();
    input.focus(function() {
        if ($.trim(input.val()) == originalvalue) {
            input.val('');
        }
    });
    input.blur(function() {
        if ($.trim(input.val()) == '') {
            input.val(originalvalue);
        }
    });
}

```
## 列高度相同
```js
$(document).ready(function() {
    function equalHeight(group) {
        tallest = 0;
        group.each(function() {
            thisHeight = $(this).height();
            if (thisHeight > tallest) {
                tallest = thisHeight;
            }
        });
        group.height(tallest);
    }
    $(document).ready(function() {
        equalHeight($(".left"));
        equalHeight($(".right"));
    });
});

```
## 获得鼠标指针XY值 
```js
$(document).ready(function() {
    $().mousemove(function(e) {
        $('#XY').html("X Axis : " + e.pageX + " | Y Axis " + e.pageY);
    });
});

```
## 返回顶部按钮
```js
$('a.top').click(function() {
    $(document.body).animate({
        scrollTop: 0
    }, 800);
    return false;
});

```
## 检查图片是否加载完成
```js
$('img').load(function() {
    console.log('image load successful');
});

```
## 自动修改破损图像
```js
$('img').on('error', function() {
    $(this).prop('src', 'img/broken.png');
});

```
## 鼠标悬停(hover)切换 class 属性
```js
$('.btn').hover(function() {
    $(this).addClass('hover');
}, function() {
    $(this).removeClass('hover');
});
$('.btn').hover(function() {
    $(this).toggleClass('hover');
});

```
## 禁用 input 字段 
```js
$('input[type="submit"]').prop('disabled', true);
$('input[type="submit"]').removeAttr('disabled');

```
## 阻止链接加载
```js
$('a.no-link').click(function(e) {
    e.preventDefault();
});

```
## 切换 fade/slide
```js
$('.btn').click(function() {
    $('.element').fadeToggle('slow');
});
$('.btn').click(function() {
    $('.element').slideToggle('slow');
});

```
## jQuery延时加载功能
```js
$(document).ready(function() {
    window.setTimeout(function() {}, 1000);
});

```
## 验证元素是否存在于jquery对象集合中
```js
$(document).ready(function() {
    if ($('#id').length) {}
});

```
## 克隆对象
```js
$(document).ready(function() {
    var cloned = $('#id').clone();
});

```
## 使元素居屏幕中间位置 
```js
$(document).ready(function() {
    jQuery.fn.center = function() {
        this.css("position", "absolute");
        this.css("top", ($(window).height() - this.height()) / 2 + $(window).scrollTop() + "px");
        this.css("left", ($(window).width() - this.width()) / 2 + $(window).scrollLeft() + "px");
        return this;
    }
    $("#id").center();
});

```
## 写自己的选择器
```js
$(document).ready(function() {
    $.extend($.expr[':'], {
        moreThen1000px: function(a) {
            return $(a).width() > 1000;
        }
    });
    $('.box:moreThen1000px').click(function() {
        alert('The element that you have clicked is over 1000 pixels wide');
    });
});

```
## 统计元素个数
```js
$(document).ready(function() {
    $("p").size();
});

```
## 禁用Jquery（动画）效果
```js
$(document).ready(function() {
    jQuery.fx.off = true;
});

```
## 与其他Javascript类库冲突解决方案
```js
$(document).ready(function() {
    var $jq = jQuery.noConflict();
    $jq('#id').show();
});