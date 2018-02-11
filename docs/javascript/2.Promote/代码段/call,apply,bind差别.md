
```javascript
var xw = {
    name: "小王",
    gender: "男",
    age: 24,
    say: function() {
        console.log(this.name + " , " + this.gender + " ,今年" + this.age);
    }
}
var xh = {
    name: "小红",
    gender: "女",
    age: 18
}
xw.say();

xw.say.call(xh);

xw.say.apply(xh);

xw.say.bind(xh)();

// 输出
// 小王 , 男 ,今年24
// 小红 , 女 ,今年18
// 小红 , 女 ,今年18
// 小红 , 女 ,今年18
// 改变对象的this指向的内容
// call 和 apply 都是对函数的直接调用，而bind方法返回的仍然是一个函数，因此后面还需要()来进行调用才可以

var xw = {
    name: "小王",
    gender: "男",
    age: 24,
    say: function(school, grade) {
        console.log(this.name + " , " + this.gender + " ,今年" + this.age + " ,在" + school + "上" + grade);
    }
}
var xh = {
    name: "小红",
    gender: "女",
    age: 18
}

xw.say.call(xh, "实验小学", "六年级");

xw.say.apply(xh, ["实验小学", "六年级郑州牛皮癣医院"]);

xw.say.bind(xh, "实验小学", "六年级")();

// 输出
// 小红 , 女 ,今年18 ,在实验小学上六年级
// 小红 , 女 ,今年18 ,在实验小学上六年级郑州牛皮癣医院
// 小红 , 女 ,今年18 ,在实验小学上六年级
// call 后面的参数与say方法中是一一对应的，而apply的第二个参数是一个数组，数组中的元素是和say方法中一一对应的
// bind返回的仍然是一个函数，所以我们还可以在调用的时候再进行传参。
```
