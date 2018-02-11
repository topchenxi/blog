
```javascript

	$(document).ready(function() {
		
		window.browser = {};
		//获取炉冷却信息字符串
		var ua = navigator.userAgent.toLowerCase();
		//浏览器信息数组，浏览器名称+版本号
		var s;
		//不同浏览器将输出一下浏览器信息
		// alert(ua);
		console.log(ua);
		// 输入结果例如：
		// 谷歌浏览器
		// mozilla/5.0 (windows nt 10.0; wow64) applewebkit/537.36 (khtml, like gecko) chrome/46.0.2490.86 safari/537.36
		// 火狐浏览器
		// mozilla/5.0 (windows nt 10.0; wow64; rv:45.0) gecko/20100101 firefox/45.0
		// IE
		// mozilla/5.0 (compatible; msie 9.0; windows nt 6.1; wow64; trident/5.0; slcc2; .net clr 2.0.50727; .net clr 3.5.30729; .net clr 3.0.30729; .net4.0c)

		//如果存在,IE
		if ((/msie ([\d.]+)/).test(ua)) {
			browser.value = ua.match(/msie ([\d.]+)/);
			browser.version = browser.value[1]; //9.0
		}
		//如果存在,firefox
		if ((/firefox\/([\d.]+)/).test(ua)) {
			browser.value = ua.match(/firefox\/([\d.]+)/);
			browser.version = browser.value[1]; //36.0
		} //如果存在,chrome
		if ((/chrome\/([\d.]+)/).test(ua)) {
			browser.value = ua.match(/chrome\/([\d.]+)/);
			browser.version = browser.value[1]; //42.0.2311.135
		} //如果存在,safari
		if ((/version\/([\d.]+).*safari/).test(ua)) {
			browser.value = ua.match(/version\/([\d.]+).*safari/);
			browser.version = browser.value[1]; //5.1.7
		}
		// alert(browser.version); //输出版本号
		console.log(browser.version)


	})

```
