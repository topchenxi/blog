# javascript 缩写技巧

## 三元操作符

当想写if...else语句时，使用三元操作符来代替。

```javascript
if (x > 10) {
    answer = 'is greater';
} else {
    answer = 'is lesser';
}
```

简写后:

```javascript
x > 10 ? 'is greater' : 'is lesser';
```

## 短路求值简写方式

当给一个变量分配另一个值时，想确定源始值不是null，undefined或空值。可以写撰写一个多重条件的if语句。
```javascript
if (variable1 !== null || variable1 !== undefined || variable1 !== '') {
     let variable2 = variable1;
}
```

简写后:
```javascript
const variable2 = variable1  || 'new';
```

## 声明变量简写方法
```javascript
let x;
let y;
let z = 3;
```

简写后:
```javascript
let x, y, z=3;


```
## if存在条件简写方法

```javascript
if (likeJavaScript === true)
```

简写后:
```javascript
if (likeJavaScript)
```

## JavaScript循环简写方法
```javascript
for (let i = 0; i < allImgs.length; i++)
```

```javascript
for (let index in allImgs)

[2, 5, 9].forEach();

```

## 短路评价

给一个变量分配的值是通过判断其值是否为null或undefined，则可以：
```javascript
let dbHost;
if (process.env.DB_HOST) {
  dbHost = process.env.DB_HOST;
} else {
  dbHost = 'localhost';
}
```

简写后:

```javascript
const dbHost = process.env.DB_HOST || 'localhost';
```

## 对象属性简写
如果属性名与key名相同，则可以采用ES6的方法：

```javascript
const obj = { x:x, y:y };
```
简写后:

```javascript
const obj = { x, y };
```
## 箭头函数简写
传统函数编写方法很容易让人理解和编写，但是当嵌套在另一个函数中，则这些优势就荡然无存。

```javascript
function sayHello(name) {
  console.log('Hello', name);
}

setTimeout(function() {
  console.log('Loaded')
}, 2000);

list.forEach(function(item) {
  console.log(item);
});

```
简写后:

```javascript
sayHello = name => console.log('Hello', name);

setTimeout(() => console.log('Loaded'), 2000);

list.forEach(item => console.log(item));
```

## 隐式返回值简写
经常使用return语句来返回函数最终结果，一个单独语句的箭头函数能隐式返回其值（函数必须省略{}为了省略return关键字）

为返回多行语句（例如对象字面表达式），则需要使用()包围函数体。

```javascript
function calcCircumference(diameter) {
  return Math.PI * diameter
}

var func = function func() {
  return { foo: 1 };
};
```
简写后:

```javascript

calcCircumference = diameter => (
  Math.PI * diameter;
)

var func = () => ({ foo: 1 });
```

## 默认参数值

为了给函数中参数传递默认值，通常使用if语句来编写，但是使用ES6定义默认值，则会很简洁：

```javascript
function volume(l, w, h) {
  if (w === undefined)
    w = 3;
  if (h === undefined)
    h = 4;
  return l * w * h;
}
```
简写后:

```javascript
volume = (l, w = 3, h = 4 ) => (l * w * h);

volume(2) //output: 24
```

## 解构赋值简写方法
在web框架中，经常需要从组件和API之间来回传递数组或对象字面形式的数据，然后需要解构它

```javascript
const observable = require('mobx/observable');
const action = require('mobx/action');
const runInAction = require('mobx/runInAction');

const store = this.props.store;
const form = this.props.form;
const loading = this.props.loading;
const errors = this.props.errors;
const entity = this.props.entity;

```
简写后:
```javascript
import { observable, action, runInAction } from 'mobx';

const { store, form, loading, errors, entity } = this.props;
也可以分配变量名：

const { store, form, loading, errors, entity:contact } = this.props;
//最后一个变量名为contact
```

## 扩展运算符简写
扩展运算符有几种用例让JavaScript代码更加有效使用，可以用来代替某个数组函数。

```javascript
// joining arrays
const odd = [1, 3, 5];
const nums = [2 ,4 , 6].concat(odd);

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = arr.slice()
```

简写后:
```javascript
// joining arrays
const odd = [1, 3, 5 ];
const nums = [2 ,4 , 6, ...odd];
console.log(nums); // [ 2, 4, 6, 1, 3, 5 ]

// cloning arrays
const arr = [1, 2, 3, 4];
const arr2 = [...arr];
// 不像concat()函数，可以使用扩展运算符来在一个数组中任意处插入另一个数组。

const odd = [1, 3, 5 ];
const nums = [2, ...odd, 4 , 6];
// 也可以使用扩展运算符解构：

```
## 强制参数简写
JavaScript中如果没有向函数参数传递值，则参数为undefined。为了增强参数赋值，可以使用if语句来抛出异常，或使用强制参数简写方法。
```javascript
function foo(bar) {
  if(bar === undefined) {
    throw new Error('Missing parameter!');
  }
  return bar;
}
```
简写后:
```javascript
mandatory = () => {
  throw new Error('Missing parameter!');
}

foo = (bar = mandatory()) => {
  return bar;
}
```
