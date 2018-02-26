# call,apply,bind差别

## 差别
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

## bind

```js
Function.prototype.bind = function(context){
  self = this;  //保存this，即调用bind方法的目标函数
  return function(){
      return self.apply(context,arguments);
  };
};
```

函数柯里化

```js
Function.prototype.bind = function(context){
  var args = Array.prototype.slice.call(arguments, 1),
  self = this;
  return function(){
      var innerArgs = Array.prototype.slice.call(arguments);
      var finalArgs = args.concat(innerArgs);
      return self.apply(context,finalArgs);
  };
};
```

```js
Function.prototype.bind = function(context){
  var args = Array.prototype.slice(arguments, 1),
  F = function(){},
  self = this,
  bound = function(){
      var innerArgs = Array.prototype.slice.call(arguments);
      var finalArgs = args.concat(innerArgs);
      return self.apply((this instanceof F ? this : context), finalArgs);
  };

  F.prototype = self.prototype;
  bound.prototype = new F();
  retrun bound;
};
```

```js
Function.prototype.bind = function (oThis) {
    if (typeof this !== "function") {
      throw new TypeError("Function.prototype.bind - what is trying to be bound is not callable");
    }

    var aArgs = Array.prototype.slice.call(arguments, 1), 
        fToBind = this, 
        fNOP = function () {},
        fBound = function () {
          return fToBind.apply(
              this instanceof fNOP && oThis ? this : oThis || window,
              aArgs.concat(Array.prototype.slice.call(arguments))
          );
        };

    fNOP.prototype = this.prototype;
    fBound.prototype = new fNOP();

    return fBound;
  };
```