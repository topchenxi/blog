# Object.defineProperty

## defineProperty介绍
```js
var myObject = {};
var nameValue = 'saving';
Object.defineProperty(myObject, 'name', {
    // true : 该属性描述符才能够被改变 和 删除。默认为 false
    'configurable': true,
    // true : 该属性才能够出现在对象的枚举属性中。默认为 false。
    'enumerable': true,
    // true : value才能被赋值运算符改变。默认为 false。 和 value 想冲突 两者只能选一个设置
    // 'writable': true,
    // 给属性提供 getter 的方法
    get() {
        return nameValue;
    },
    // 给属性提供 setter 的方法
    set(val) {
        nameValue = val;
    }
})
myObject.autor = 'saving';
console.log(myObject)
for (let key in myObject) {
    // 默认情况下通过defineProperty定义的属性是不能被枚举(遍历)的
    // 需要设置enumerable为true才可以
    console.log(key);
}
// 触发setter
myObject.name = 'walking';
console.log(myObject)
```

## html结构
```html
<div id="app">
    <h1>{{author}}</h1>
    <h2>{{article.name}}</h2>
    <p>主题为{{article.type}}</p>
    <p>作者为{{author}}</p>
    <p>{{whole}}</p>
    <input v-model="author" type="text">
</div>
<script src="./js/index.js"></script>
<script>
let mvvm = new Mvvm({
    el: '#app',
    data: {
        author: 'saving',
        article: {
            name: 'Object.defineProperty',
            type: 'vue'
        },
        reader: 'walking'
    },
    computed: {
        whole() {
            return this.author + ' ' + this.article.type;
        }
    },
    mounted: function() {
        console.log('Finish');
    }
});
</script>
```

## 创建一个Mvvm构造函数
```js
// 创建一个Mvvm构造函数
// 这里用es6方法将options赋一个初始值，防止没传，等同于options || {}
function Mvvm(options = {}) {
	// vm.$options Vue上是将所有属性挂载到上面
	// 所以我们也同样实现,将所有属性挂载到了$options
	this.$options = options;
	// this._data 这里也和Vue一样
	let data = this._data = this.$options.data;
	// 数据劫持
	observe(data);
	// 回归对象
	// this 代理了this._data
	for (let key in data) {
		Object.defineProperty(this, key, {
			configurable: true,
			get() {
				return this._data[key]; // 如this.a = {b: 1}
			},
			set(newVal) {
				this._data[key] = newVal;
			}
		});
	}
	// 初始化computed,将this指向实例
	initComputed.call(this);
	// 编译    
	new Compile(options.el, this);
	// 所有事情处理好后执行mounted钩子函数
	options.mounted.call(this); // 这就实现了mounted钩子函数
}
```

## 数据劫持
```js
function Observe(data) {
	// 所谓数据劫持就是给对象增加get,set
	// 先遍历一遍对象再说
	let dep = new Dep();
	for (let key in data) { // 把data属性通过defineProperty的方式定义属性
		let val = data[key];
		observe(val); // 递归继续向下找，实现深度的数据劫持
		Object.defineProperty(data, key, {
			configurable: true,
			get() {
				Dep.target && dep.addSub(Dep.target); // 将watcher添加到订阅事件中 [watcher]
				return val;
			},
			set(newVal) { // 更改值的时候
				if (val === newVal) { // 设置的值和以前值一样就不理它
					return;
				}
				val = newVal; // 如果以后再获取值(get)的时候，将刚才设置的值再返回去
				observe(newVal); // 当设置为新值后，也需要把新值再去定义成属性
				dep.notify(); // 让所有watcher的update方法执行即可
			}
		});
	}
}

// 外面再写一个函数
// 不用每次调用都写个new
// 也方便递归调用
function observe(data) {
	// 如果不是对象的话就直接return掉
	// 防止递归溢出
	if (!data || typeof data !== 'object') return;
	return new Observe(data);
}
```

## 创建Compile构造函数
```js
// 创建Compile构造函数
function Compile(el, vm) {
	// 将el挂载到实例上方便调用
	vm.$el = document.querySelector(el);
	// 在el范围里将内容都拿到，当然不能一个一个的拿
	// 可以选择移到内存中去然后放入文档碎片中，节省开销
	let fragment = document.createDocumentFragment();

	while (child = vm.$el.firstChild) {
		fragment.appendChild(child); // 此时将el中的内容放入内存中
	}
	// 对el里面的内容进行替换
	function replace(frag) {
		Array.from(frag.childNodes).forEach(node => {
			let txt = node.textContent;
			let reg = /\{\{(.*?)\}\}/g; // 正则匹配{{}}

			if (node.nodeType === 3 && reg.test(txt)) { // 即是文本节点又有大括号的情况{{}}
				// console.log(RegExp.$1); 
				// 匹配到的第一个分组 如： a.b, c
				let arr = RegExp.$1.split('.');
				let val = vm;
				arr.forEach(key => {
					val = val[key]; // 如this.a.b
				});
				// 用trim方法去除一下首尾空格
				node.textContent = txt.replace(reg, val).trim();
				// 监听变化
				// 给Watcher再添加两个参数，用来取新的值(newVal)给回调函数传参
				new Watcher(vm, RegExp.$1, newVal => {
					node.textContent = txt.replace(reg, newVal).trim();
				});
			}
			if (node.nodeType === 1) { // 元素节点
				let nodeAttr = node.attributes; // 获取dom上的所有属性,是个类数组
				Array.from(nodeAttr).forEach(attr => {
					let name = attr.name; // v-model  type
					let exp = attr.value;
					if (name.includes('v-')) {
						node.value = vm[exp];
					}
					// 监听变化
					new Watcher(vm, exp, function(newVal) {
						node.value = newVal; // 当watcher触发时会自动将内容放进输入框中
					});

					node.addEventListener('input', e => {
						let newVal = e.target.value;
						// 相当于给this.c赋了一个新值
						// 而值的改变会调用set，set中又会调用notify，notify中调用watcher的update方法实现了更新
						vm[exp] = newVal;
					});
				});
			}

			// 如果还有子节点，继续递归replace
			if (node.childNodes && node.childNodes.length) {
				replace(node);
			}
		});
	}
	replace(fragment); // 替换内容
	vm.$el.appendChild(fragment); // 再将文档碎片放入el中
}

```

## 发布订阅模式
```js
// 发布订阅模式  订阅和发布 如[fn1, fn2, fn3]
function Dep() {
	// 一个数组(存放函数的事件池)
	this.subs = [];
}
Dep.prototype = {
	addSub(sub) {
		this.subs.push(sub);
	},
	notify() {
		// 绑定的方法，都有一个update方法
		this.subs.forEach(sub => sub.update());
	}
};
// 监听函数
// 通过Watcher这个类创建的实例，都拥有update方法
function Watcher(fn) {
	this.fn = fn; // 将fn放到实例上
}

// 重写Watcher构造函数
function Watcher(vm, exp, fn) {
	this.fn = fn;
	this.vm = vm;
	this.exp = exp;
	// 添加一个事件
	// 这里我们先定义一个属性
	Dep.target = this;
	let arr = exp.split('.');
	let val = vm;
	arr.forEach(key => { // 取值
		val = val[key]; // 获取到this,默认就会调用get方法
	});
	Dep.target = null;
}

Watcher.prototype.update = function() {
	// notify的时候值已经更改了
	// 再通过vm, exp来获取新的值
	let arr = this.exp.split('.');
	let val = this.vm;
	arr.forEach(key => {
		val = val[key]; // 通过get获取到新的值
	});
	this.fn(val); // 将每次拿到的新值去替换{{}}的内容即可
};

// 数据更新视图

```

## 定义钩子函数(computed)
```js
// computed(计算属性)
function initComputed() {
	let vm = this;
	let computed = this.$options.computed; 
	// 从options上拿到computed属性
	// 得到的都是对象的key可以通过Object.keys转化为数组
	Object.keys(computed).forEach(key => {
		Object.defineProperty(vm, key, {
			// 这里判断是computed里的key是对象还是函数
			// 如果是函数直接就会调get方法
			// 如果是对象的话，手动调一下get方法即可
			// 所以不需要new Watcher去监听变化了
			get: typeof computed[key] === 'function' ? computed[key] : computed[key].get,
			set() {}
		});
	});
}
```