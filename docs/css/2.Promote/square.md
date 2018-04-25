# 正方形

## 方法1
```html
<style>
.square {
    width: 50%;
    /*避免被内容撑开多余的高度*/
    height: 0;
    /* padding百分比相对父元素宽度计算 */
    padding-bottom: 50%;
}
</style>
<div class="square"></div>
```

## 方法2
```html
<style>
.square {
    width: 20%;
    background: #ccc;
}
.square:after {
    display: block;
    padding-bottom: 100%;
    content: '';
}
.content {
    position: absolute;
    width: 100%;
    height: 100%;
}
</style>
<div class="square">
    <div class="content">
        Hello!
    </div>
</div>
```

## 方法3
```html
<style>
.vw {
    width: 10%;
    /* 1vw = 1% viewport width */
    height: 10vw;
    background: #ccc;
}
</style>
<div class="vw">hello,viewport</div>
```