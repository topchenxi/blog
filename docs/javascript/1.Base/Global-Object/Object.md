# Object

`Object` 构造函数为给定值创建一个对象包装器。

## Object 方法
```js
Object.assign()  // 通过复制一个或多个对象来创建一个新的对象。
Object.create()  // 使用指定的原型对象和属性创建一个新对象。
Object.defineProperty()  // 给对象添加一个属性并指定该属性的配置。
Object.defineProperties()  // 给对象添加多个属性并分别指定它们的配置。
Object.entries()  // 返回给定对象自身可枚举属性的[key, value]数组。
Object.freeze()  // 冻结对象：其他代码不能删除或更改任何属性。
Object.getOwnPropertyDescriptor()  // 返回对象指定的属性配置。
Object.getOwnPropertyNames()  // 返回一个数组，它包含了指定对象所有的可枚举或不可枚举的属性名。
Object.getOwnPropertySymbols()  // 返回一个数组，它包含了指定对象自身所有的符号属性。
Object.getPrototypeOf()  // 返回指定对象的原型对象。
Object.is()  // 比较两个值是否相同。所有 NaN 值都相等（这与==和===不同）。
Object.isExtensible()  // 判断对象是否可扩展。
Object.isFrozen()  // 判断对象是否已经冻结。
Object.isSealed()  // 判断对象是否已经密封。
Object.keys()  // 返回一个包含所有给定对象自身可枚举属性名称的数组。
Object.preventExtensions()  // 防止对象的任何扩展。
Object.seal()  // 防止其他代码删除对象的属性。
Object.setPrototypeOf()  // 设置对象的原型（即内部[[Prototype]]属性）。
Object.values()  // 返回给定对象自身可枚举值的数组。
```


## 判断Object类型

```js
var objectTypes = {
    'boolean': false,
    'function': true,
    'object': true,
    'number': false,
    'string': false,
    'undefined': false
};
function isObject(value) {
    return !!(value && objectTypes[typeof value]);
}
```

## 判断类型
```js
function kindOf(val) {
    if (typeof val === 'undefined') {
        return 'undefined';
    }
    if (val === null) {
        return 'null';
    }
    if (val === true || val === false || val instanceof Boolean) {
        return 'boolean';
    }
    if (typeof val === 'string' || val instanceof String) {
        return 'string';
    }
    if (typeof val === 'number' || val instanceof Number) {
        return 'number';
    }
    if (typeof val === 'function' || val instanceof Function) {
        return 'function';
    }
    if (typeof Array.isArray !== 'undefined' && Array.isArray(val)) {
        return 'array';
    }
    if (val instanceof RegExp) {
        return 'regexp';
    }
    if (val instanceof Date) {
        return 'date';
    }
    var type = toString.call(val);
    if (type === '[object Array]') {
        return 'array';
    }
    if (type === '[object RegExp]') {
        return 'regexp';
    }
    if (type === '[object Date]') {
        return 'date';
    }
    if (type === '[object Arguments]') {
        return 'arguments';
    }
    if (type === '[object Error]') {
        return 'error';
    }
    if (type === '[object Set]') {
        return 'set';
    }
    if (type === '[object WeakSet]') {
        return 'weakset';
    }
    if (type === '[object Map]') {
        return 'map';
    }
    if (type === '[object WeakMap]') {
        return 'weakmap';
    }
    if (type === '[object Symbol]') {
        return 'symbol';
    }
    if (type === '[object Int8Array]') {
        return 'int8array';
    }
    if (type === '[object Uint8Array]') {
        return 'uint8array';
    }
    if (type === '[object Uint8ClampedArray]') {
        return 'uint8clampedarray';
    }
    if (type === '[object Int16Array]') {
        return 'int16array';
    }
    if (type === '[object Uint16Array]') {
        return 'uint16array';
    }
    if (type === '[object Int32Array]') {
        return 'int32array';
    }
    if (type === '[object Uint32Array]') {
        return 'uint32array';
    }
    if (type === '[object Float32Array]') {
        return 'float32array';
    }
    if (type === '[object Float64Array]') {
        return 'float64array';
    }
    return 'object';
};
```

## 判断具体类型
```js
function getType(a) {
    var typeArray = Object.prototype.toString.call(a).split(" ");
    return typeArray[1].slice(0, this.length - 1);
}
```