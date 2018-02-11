
```javascript
	/*

		Location 对象
		Location 对象包含有关当前 URL 的信息。
		Location 对象是 Window 对象的一个部分，可通过 window.location 属性来访问。

	*/

	// Location 对象属性
	// hash	设置或返回从井号 (#) 开始的 URL（锚）。
	console.log("hash : " + window.location.hash);

	// 例子：http://sit1.seller.e-cantonfair.com/seller_center/sellerShop/toSellerShop.cf

	// host	返回主机名和当前 URL 的端口号。
	console.log("host : " + window.location.host);
	// 结果：host : sit1.seller.e-cantonfair.com

	// hostname	返回当前 URL 的主机名。
	console.log("hostname : " + window.location.hostname);
	// 结果：hostname : sit1.seller.e-cantonfair.com

	// href	返回完整的 URL。
	console.log("href : " + window.location.href);
	// 结果：href : http://sit1.seller.e-cantonfair.com/seller_center/sellerShop/toSellerShop.cf?status=1

	// pathname	返回当前 URL 的路径部分。
	console.log("pathname : " + window.location.pathname);
	// 结果：pathname : /seller_center/sellerShop/toSellerShop.cf

	// port	返回当前 URL 的端口号。
	console.log("port : " + window.location.port);
	// 结果：port : 

	// protocol	返回当前 URL 的协议。
	console.log("protocol : " + window.location.protocol);
	// 结果：protocol : http:

	// search	返回从问号 (?) 开始的 URL（查询部分）。
	console.log("search : " + window.location.search);
	// 结果：search : ?status=1

	// 设置
	// window.location.host="sit1.seller.e-cantonfair.com";
	// window.location.hostname="sit1.seller.e-cantonfair.com";
	// window.location.href="http://www.baidu.com";

	// Location 对象方法

	// assign(URL)	加载新的文档。
	// window.location.assign("http://www.baidu.com")

	// reload()	重新加载当前文档。
	// window.location.reload()

	// replace(newURL)	用新的文档替换当前文档。(不会在 History 对象中生成一个新的记录)
	// window.location.replace("http://www.baidu.com")

```
