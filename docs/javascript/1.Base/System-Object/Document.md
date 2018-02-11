
```javascript

	// HTML DOM Document 对象
	// Document 对象
	// 每个载入浏览器的 HTML 文档都会成为 Document 对象。
	// Document 对象使我们可以从脚本中对 HTML 页面中的所有元素进行访问。

	// Document 对象集合

	// all[]	提供对文档中所有 HTML 元素的访问。
	console.log(window.document.all);

	// anchors[]	返回对文档中所有 Anchor 对象的引用。
	console.log(window.document.anchors);

	// applets	返回对文档中所有 Applet 对象的引用。
	console.log(window.document.applets);

	// forms[]	返回对文档中所有 Form 对象引用。
	console.log(window.document.forms);

	// images[]	返回对文档中所有 Image 对象引用。
	console.log(window.document.images);

	// links[]	返回对文档中所有 Area 和 Link 对象引用。
	console.log(window.document.links);

	// Document 对象属性
	// body	提供对 <body> 元素的直接访问。
	console.log("body : " + window.document.body);

	// cookie	设置或返回与当前文档有关的所有 cookie。
	console.log("cookie : " + window.document.cookie);

	// domain	返回当前文档的域名。
	console.log("domain : " + window.document.domain);

	// lastModified	返回文档被最后修改的日期和时间。
	console.log("lastModified : " + window.document.lastModified);

	// referrer	返回载入当前文档的文档的 URL。
	console.log("referrer : " + window.document.referrer);

	// title	返回当前文档的标题。
	console.log("title : " + window.document.title);

	// URL	返回当前文档的 URL。
	console.log("URL : " + window.document.URL);

	// Document 对象方法
	// 方法	描述

	// getElementById()	返回对拥有指定 id 的第一个对象的引用。
	// <div class="site-nav" id="site-nav"></div>
	console.log(window.document.getElementById("site-nav"));


	// getElementsByName()	返回带有指定名称的对象集合。
	// <input type="text" name="keyword" id="keyword" placeholder="What are you looking for..." autocomplete="off">
	console.log(window.document.getElementsByName("keyword"));

	// getElementsByTagName()	返回带有指定标签名的对象集合。返回元素的顺序是它们在文档中的顺序。
	console.log(window.document.getElementsByTagName("input"));

	// open()	打开一个流，以收集来自任何 document.write() 或 document.writeln() 方法的输出。
	console.log()
	
	// write()	向文档写 HTML 表达式 或 JavaScript 代码。
	// document.write("");

	// writeln()	等同于 write() 方法，不同的是在每个表达式之后写一个换行符。

```
