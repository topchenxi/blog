# 注意事项

## 函数

`anguments`

`anguments.length`  实际传入函数参数的个数
`anguments.callee`  指向拥有这个anguments对象的(严格模式报错)

`this`
    箭头函数无 this

`fnName.caller`  保存着调用当前函数的函数的引用，如果在全局作用域调用当前函数，则返回 `null`

`fnName.length` 表示函数希望接收的命名参数的个数

`fnName.name` (es6) 获取函数的函数名

`fnName.apply` `fnName.call`
上面两个方法都用来在特殊的作用域调用函数，实际上等于设置函数体内的 `this` 对象的值
`apply` 接收 `anguments` 对象或数组，`call` 必须逐个列举出来

`fnName.bind()`
根据已有函数，创建一个被绑定新 `this` 值的函数


箭头函数有几点需要注意：

函数体内的 `this` 对象是函数定义是所在的对象，而不是使用时的对象
不能用箭头函数当做构造函数，也就是说不能使用new命令，否则会报错
不可以使用 `arguments` 对象，该对象在函数体内不存在。如果要用，可以用 `Rest参数` 代替。
不可以使用 `yield` 命令，因此箭头函数不能用作 `Generator` 函数。
由于箭头函数没有自己的 `this`，所以当然也就不能用 `call()`、`apply()`、`bind()` 这些方法去改变 `this` 的指向。

