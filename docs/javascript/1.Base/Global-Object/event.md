# event

## api


```javascript
// 事件句柄
$('body').on('onabort', '.selector', function(event) {
    event.preventDefault();
    // do something
});
document.querySelector('p').onclick = function() {
	// do something
}

// onblur	元素失去焦点	
// onchange	用户改变域的内容
// onclick	鼠标点击某个对象
// ondblclick	鼠标双击某个对象	
// onerror	当加载文档或图像时发生某个错误	
// onfocus	元素获得焦点	
// onkeydown	某个键盘的键被按下		
// onkeypress	某个键盘的键被按下或按住	
// onkeyup	某个键盘的键被松开	
// onload	某个页面或图像被完成加载
// onmousedown	某个鼠标按键被按下
// onmousemove	鼠标被移动	
// onmouseout	鼠标从某元素移开
// onmouseover	鼠标被移到某元素之上
// onmouseup	某个鼠标按键被松开	
// onreset	重置按钮被点击	
// onresize	窗口或框架被调整尺寸	
// onselect	文本被选定	
// onsubmit	提交按钮被点击	
// onunload	用户退出页面		
```

## 元素事件绑定 兼容任何浏览器
```js
function eventBind(obj, eventType, callBack) {
    if (obj.addEventListener) {
        obj.addEventListener(eventType, callBack, false);
    } else if (window.attachEvent) {
        obj.attachEvent('on' + eventType, callBack);
    } else {
        obj['on' + eventType] = callBack;
    }
};
eventBind(document, 'click', bodyClick);
```

## 元素移除事件 兼容任何浏览器

```js
function moveBind(objId, eventType, callBack) {
    var obj = document.getElementById(objId);
    if (obj.removeEventListener) {
        obj.removeEventListener(eventType, callBack, false);
    } else if (window.detachEvent) {
        obj.detachEvent('on' + eventType, callBack);
    } else {
        obj['on' + eventType] = null;
    }
}
```
