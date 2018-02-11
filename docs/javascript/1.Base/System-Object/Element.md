
```javascript

	// HTML DOM Element 对象
	// HTML DOM 节点
	// 在 HTML DOM （文档对象模型）中，每个部分都是节点：
	// 文档本身是文档节点
	// 所有 HTML 元素是元素节点
	// 所有 HTML 属性是属性节点
	// HTML 元素内的文本是文本节点


	/*
		<div class="test-class1 test-class2" id="test-id" data-id="11" data-index="22">Hello world!</div>
	*/

	var myElement = window.document.getElementById("test-id");

	console.log(myElement);
	// element.accessKey	设置或返回元素的快捷键。
	console.log(myElement.accessKey);

	// element.appendChild()	向元素添加新的子节点，作为最后一个子节点。

	// element.attributes	返回元素属性的 NamedNodeMap。
	console.log(myElement.attributes);
	console.log(myElement.attributes["class"]);

	// element.childNodes	返回元素子节点的 NodeList。
	console.log(myElement.childNodes);

	// element.className	设置或返回元素的 class 属性。
	console.log(myElement.className);

	// element.clientHeight	返回元素的可见高度。
	console.log(myElement.clientHeight);

	// element.clientWidth	返回元素的可见宽度。
	console.log(myElement.clientWidth);

	// element.cloneNode()	克隆元素。

	// element.compareDocumentPosition()	比较两个元素的文档位置。

	// element.contentEditable	设置或返回元素的文本方向。
	console.log(myElement.contentEditable);

	// element.dir	设置或返回元素的文本方向。
	console.log(myElement.dir);

	// element.firstChild	返回元素的首个子。
	console.log(myElement.firstChild);

	// element.getAttribute()	返回元素节点的指定属性值。
	console.log(myElement.getAttribute("data-id"));

	// element.getAttributeNode()	返回指定的属性节点。
	console.log(myElement.getAttributeNode("data-id"));

	// element.hasAttribute()	如果元素拥有指定属性，则返回true，否则返回 false。
	console.log(myElement.hasAttribute("data-id"));

	// element.hasAttributes()	如果元素拥有属性，则返回 true，否则返回 false。
	console.log(myElement.hasAttributes("data-id"));

	// element.hasChildNodes()	如果元素拥有子节点，则返回 true，否则 false。
	console.log(myElement.hasChildNodes());

	// element.id	设置或返回元素的 id。
	console.log(myElement.id);

	// element.innerHTML	设置或返回元素的内容。
	console.log(myElement.innerHTML);

	// element.isContentEditable	设置或返回元素的内容。
	console.log(myElement.isContentEditable);

	// element.isEqualNode()	检查两个元素是否相等。

	// element.isSameNode()	检查两个元素是否是相同的节点。

	// element.isSupported()	如果元素支持指定特性，则返回 true。

	// element.lang	设置或返回元素的语言代码。
	console.log(myElement.lang);

	// element.lastChild	返回元素的最后一个子元素。
	console.log(myElement.lastChild);

	// element.namespaceURI	返回元素的 namespace URI。
	console.log(myElement.namespaceURI);

	// element.nextSibling	返回位于相同节点树层级的下一个节点。
	console.log(myElement.nextSibling);

	// element.nodeName	返回元素的名称。
	console.log(myElement.nodeName);

	// element.nodeType	返回元素的节点类型。
	console.log(myElement.nodeType);

	// element.nodeValue	设置或返回元素值。
	console.log(myElement.nodeValue);

	// element.normalize()	合并元素中相邻的文本节点，并移除空的文本节点。

	// element.offsetHeight	返回元素的高度。
	console.log("高度:" + myElement.offsetHeight);

	// element.offsetWidth	返回元素的宽度。
	console.log("宽度:" + myElement.offsetWidth);

	// element.offsetLeft	返回元素的水平偏移位置。
	console.log("水平偏移位置:" + myElement.offsetLeft);

	// element.offsetTop	返回元素的垂直偏移位置。
	console.log("垂直偏移位置:" + myElement.offsetTop);

	// element.scrollHeight	返回元素的整体高度。
	console.log("整体高度:" + myElement.scrollHeight);

	// element.scrollWidth	返回元素的整体宽度。
	console.log("整体宽度:" + myElement.scrollWidth);

	// element.scrollLeft	返回元素左边缘与视图之间的距离。
	console.log("元素左边缘与视图之间的距离:" + myElement.scrollLeft);

	// element.scrollTop	返回元素上边缘与视图之间的距离。
	console.log("元素上边缘与视图之间的距离:" + myElement.scrollTop);

	// element.ownerDocument	返回元素的根元素（文档对象）。
	console.log("根元素:" + myElement.ownerDocument);

	// element.parentNode	返回元素的父节点。
	console.log("父节点:" + myElement.parentNode);

	// element.previousSibling	返回位于相同节点树层级的前一个元素。
	console.log("前一个元素:" + myElement.previousSibling);

	// element.style	设置或返回元素的 style 属性。
	console.log("style 属性:" + myElement.style);

	// element.tabIndex	设置或返回元素的 tab 键控制次序。
	console.log("tab 键控制次序:" + myElement.tabIndex);

	// element.tagName	返回元素的标签名。
	console.log("标签名:" + myElement.tagName);

	// element.textContent	设置或返回节点及其后代的文本内容。
	console.log("文本内容:" + myElement.textContent);

	// element.title	设置或返回元素的 title 属性。
	console.log("title:" + myElement.title);

	// element.replaceChild()	替换元素中的子节点。

	/*
		element.setAttribute()	把指定属性设置或更改为指定值。
		element.setAttributeNode()	设置或更改指定属性节点。
		element.setIdAttribute()	
		element.setIdAttributeNode()	
		element.setUserData()	把对象关联到元素上的键。
	*/

	/*	
		element.removeAttribute()	从元素中移除指定属性。
		element.removeAttributeNode()	移除指定的属性节点，并返回被移除的节点。
		element.removeChild()	从元素中移除子节点。
	*/

```
