# iscroll

[github 地址](https://github.com/cubiq/iscroll/)

## 用法
```html
<html>

<head>
    <meta http-equiv="Content-Type" content="text/html; charset=utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=0, minimum-scale=1.0, maximum-scale=1.0">
    <meta name="apple-mobile-web-app-capable" content="yes">
    <meta name="apple-mobile-web-app-status-bar-style" content="black">
    <script src="js/iscroll-master/build/iscroll-infinite.js"></script>
    <style>
    #wrapper {
        position: absolute;
        z-index: 1;
        top: 45px;
        bottom: 48px;
        left: 0;
        width: 100%;
        background: #aaa;
        overflow: auto;
    }

    #scroller {
        position: relative;
        /* -webkit-touch-callout:none;*/
        -webkit-tap-highlight-color: rgba(0, 0, 0, 0);

        float: left;
        width: 100%;
        padding: 0;
    }

    #scroller ul {
        position: relative;
        list-style: none;
        padding: 0;
        margin: 0;
        width: 100%;
        text-align: left;
    }

    #scroller li {
        padding: 0 10px;
        height: 40px;
        line-height: 40px;
        border-bottom: 1px solid #ccc;
        border-top: 1px solid #fff;
        background-color: #fafafa;
        font-size: 14px;
    }

    #scroller li>a {
        display: block;
    }
    </style>
    <title>滚动测试</title>
</head>

<body>
    <div id="wrapper">
        <div id="scroller">
            <ul id="thelist">
                <li>Pretty row 1</li>
                <li id="aaa">Pretty row 2</li>
                <li>Pretty row 3</li>
                <li>Pretty row 4</li>
                <li>Pretty row 5</li>
                <li>Pretty row 6</li>
                <li>Pretty row 7</li>
                <li>Pretty row 8</li>
                <li>Pretty row 9</li>
                <li>Pretty row 10</li>
                <li>Pretty row 11</li>
                <li>Pretty row 12</li>
                <li>Pretty row 13</li>
                <li>Pretty row 14</li>
                <li>Pretty row 15</li>
                <li>Pretty row 16</li>
                <li>Pretty row 17</li>
                <li>Pretty row 18</li>
            </ul>
        </div>
    </div>
     <!--实例化iScroll-->
    <script type="text/javascript">
    var myscroll;
    function loaded() {
        myscroll = new IScroll("#wrapper");
    }
    window.addEventListener("DOMContentLoaded", loaded, false);
    </script>
</body>

</html>
```