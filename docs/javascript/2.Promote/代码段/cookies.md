# Cookie

## 获取cookie值

```js
function getCookie(name) {
    var arr = document.cookie.match(new RegExp("(^| )" + name + "=([^;]*)(;|$)"));
    if (arr != null) return unescape(arr[2]);
    return null
}
```
```js
function getCookieValue(name) {
    // 用处理字符串的方式查找到key对应value  
    var name = escape(name);
    // 读cookie属性，这将返回文档的所有cookie  
    var allcookies = document.cookie;
    // 查找名为name的cookie的开始位置  
    name += "=";
    var pos = allcookies.indexOf(name);
    // 如果找到了具有该名字的cookie，那么提取并使用它的值  
    if (pos != -1) {
        // 如果pos值为-1则说明搜索"version="失败  
        var start = pos + name.length;
        // cookie值开始的位置  
        var end = allcookies.indexOf(";", start);
        // 从cookie值开始的位置起搜索第一个";"的位置,即cookie值结尾的位置  
        if (end == -1) end = allcookies.length;
        // 如果end值为-1说明cookie列表里只有一个cookie  
        var value = allcookies.substring(start, end);
        // 提取cookie的值  
        return (value);
        // 对它解码        
    } else {
        // 搜索失败，返回空字符串  
        return "";
    }
}
```

```js
function getCookieMethod(name) {
    return (parseCookie(document.cookie))[name];
}
function parseCookie(text, shouldDecode) {
    var cookies = {};
    if (text === 'string' && text.length > 0) {
        var cookieParts = text.split(/;\s/g),
            cookieLen = cookieParts.length,
            cookieName,
            cookieValue,
            cookieNameValue,
            i;
        for (i = 0; i < cookieLen; i++) {
            cookieNameValue = cookieParts[i].match(/([^=]+)=/i);
            if (cookieNameValue instanceof Array) {
                cookieName = decode(cookieNameValue[1]);
                cookieValue = decode(cookieParts[i].substring(cookieNameValue[1].length + 1))
            } else {
                cookieName = decode(cookieParts[i]);
                cookieValue = '';
            }
            if (cookieName) {
                cookies[cookieName] = cookieValue;
            }
        }
    }

    return cookies;
}
```

## 设置cookie值

```js
function setCookie(name, value, Hours, domain) {
    var d = new Date();
    var offset = 8;
    var utc = d.getTime() + (d.getTimezoneOffset() * 60000);
    var nd = utc + (3600000 * offset);
    var exp = new Date(nd);
    exp.setTime(exp.getTime() + Hours * 60 * 60 * 1000);
    document.cookie = name + "=" + escape(value) + ";path=/;expires=" + exp.toGMTString() + ";domain=" + domain + ";"
}

```

```js
function addCookie(name, value, days, path) {
    var name = escape(name);
    var value = escape(value);
    var expires = new Date();
    expires.setTime(expires.getTime() + days * 3600000 * 24);
    // path=/，表示cookie能在整个网站下使用，path=/temp，表示cookie只能在temp目录下使用  
    path = path == "" ? "" : ";path=" + path;
    // GMT(Greenwich Mean Time)是格林尼治平时，现在的标准时间，协调世界时是UTC  
    // 参数days只能是数字型  
    var _expires = (typeof days) == "string" ? "" : ";expires=" + expires.toUTCString();
    document.cookie = name + "=" + value + _expires + path;
}
```
```js
function setCookieMethod(name, value, options) {
    options = options || {};
    var expires = options.expires,
        domain = options.domain,
        path = options.path,
        value = encode(value),
        text = name + '=' + value,
        date = expires;
    if (typeof date === 'number') {
        date = new Date();
        date.setDate(date.getDate() + expires);
    }
    if (date instanceof Date) text += '; expires=' + date.toUTCString();
    if (domain) text += '; domain=' + domain;
    if (path) text += '; path=' + path;
    if (options['secure']) text += '; secure';
    document.cookie = text;
    return text;
}
```
## 删除Cookie
```js
function deleteCookie(name, path) {
    var name = escape(name);
    var expires = new Date(0);
    path = path == "" ? "" : ";path=" + path;
    document.cookie = name + "=" + ";expires=" + expires.toUTCString() + path;
}
```
```js
function removeCookieMethod(name, options) {
    options = options || {};
    options['expires'] = new Date(0);
    return setCookieMethod(name, '', options);
}
```
