```javascript
// 定义父类
function SuperType(name) {
    this.name = name;
}
SuperType.prototype.type = "type is SuperType";

// 定义子类
function SubType(name, age) {
    SuperType.call(this, name);
    this.age = age;
}

SubType.prototype = new SuperType();
SubType.prototype.contructor = SubType;

let obj = new SubType('Top_Chenxi', '18');

Object.defineProperty(obj, 'height', {
    'value': 180,
    'enumable': false //不可遍历
});


// 1：遍历对象可枚举的所有自身的属性
// 1.1 使用Object.key()+for..of
let Traversal_1 = (obj) => {
    for (let key of Object.keys(obj)) {
        console.log(1, key, obj[key]);
    }
};
Traversal_1(obj);
// name Top_Chenxi
// age 18

// 1.2 for..in + hasOwnProperty
let Traversal_2 = (obj) => {
    for (let key in obj) {
        if (obj.hasOwnProperty(key)) console.log(2, key, obj[key]);
    }
}
Traversal_2(obj);
// name Top_Chenxi
// age 18

// 2：遍历对象所有的（包括可枚举和不可枚举的）自身的属性
// 2.1 Object.getOwnPropertyNames()使用for..of遍历
let Traversal_3 = (obj) => {
    for (let key of Object.getOwnPropertyNames(obj)) {
        console.log(3, key, obj[key]);
    }
};
Traversal_3(obj);
// name Top_Chenxi
// age 18
// height 180

// 3：遍历对象可枚举的自身和继承的属性
// 3.1 使用for..in循环遍历
let Traversal_4 = (obj) => {
    for (key in obj) {
        console.log(4, key, obj[key]);
    }
};

Traversal_4(obj);
// name Top_Chenxi
// age 18
// contructor ...
// type type is SuperType


// 4：遍历对象所有的自身和继承的属性
// 4.1 do..while循环 
var Traversal_5 = (obj) => {
    // do语句内容至少执行一次，当while判断语句为true，反复执行
    do {
        console.log(5, Object.getOwnPropertyNames(obj))
    } while (obj = Object.getPrototypeOf(obj));
};

Traversal_5(obj);
```