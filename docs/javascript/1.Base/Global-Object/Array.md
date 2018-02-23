# Array

## 定义数组
```javascript

var ArrayLength = 5;
// 创建 Array 对象的语法：
// 没有使用参数，那么返回的数组为空，length 字段为 0。
var array1 = new Array();
// 参数 ArrayLength 是期望的数组元素个数。返回的数组，length 字段将被设为 ArrayLength 的值。
var array2 = new Array(ArrayLength);
// 参数 1,2,3 是参数列表。当使用这些参数来调用构造函数 Array() 时，新创建的数组的元素就会被初始化为这些值。
// 它的 length 字段也会被设置为参数的个数。
var array3 = new Array(1, 2, 3);

```

## 数组方法

`concat`,`join`,`pop`,`push`,`reverse`,`shift`,`slice`,`sort`,`splice`
```javascript
// concat
arr1 = arr1.concat(arr2, arr3);

// join() 把数组的所有元素放入一个字符串。 元素通过指定的分隔符进行分隔。
var arr4 = new Array(5, 1, 9, 8, 2, 7, 4, 5, 6, 1, 8);
var str1 = arr4.join('_');

// pop() 删除并返回数组的最后一个元素
arr4.pop();

// push() 向数组的末尾添加一个或更多元素， 并返回新的长度。
arr4.push(0);

// reverse() 颠倒数组中元素的顺序。
arr4.reverse();

// shift() 删除并返回数组的第一个元素
var first = arr4.shift();

// slice() 从某个已有的数组返回选定的元素
var arr5 = arr4.slice(2, 5);

// sort() 对数组的元素进行排序
arr4.sort();

// splice() 删除元素， 并向数组添加新元素。 
// arrayObject.splice(index,howmany,item1,.....,itemX)
// index	必需。整数，规定添加/删除项目的位置，使用负数可从数组结尾处规定位置。
// howmany	必需。要删除的项目数量。如果设置为 0，则不会删除项目。
// item1--itemX	可选。向数组添加的新项目。
arr4.splice(4, 3, 8, 8, 8);

// toSource() 返回该对象的源代码。 
// 只有 Gecko 核心的浏览器（比如 Firefox）支持该方法，也就是说 IE、Safari、Chrome、Opera 等浏览器均不支持该方法。

// toString() 把数组转换为字符串， 并返回结果。

// toLocaleString() 把数组转换为本地数组， 并返回结果。

// unshift() 向数组的开头添加一个或更多元素， 并返回新的长度。

// valueOf() 返回数组对象的原始值

```

## 数组去重
```js
function unique(arr) {
    var obj = {}
    var result = []
    for (var i in arr) {
        if (!obj[arr[i]]) {
            obj[arr[i]] = true;
            result.push(arr[i]);
        }
    }
    return result;
}
```

## 数组中最大差值
```js
function getMaxProfit(arr) {
    var min = arr[0],
        max = arr[0];
    for (var i = 0; i < arr.length; i++) {
        if (arr[i] < min) min = arr[i];
        if (arr[i] > max) max = arr[i];
    }
    return max - min;
}
```
