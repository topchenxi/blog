### [基础] angular 内置命令介绍

内置指令
1.`ng-href`
2.`ng-src`
3.`ng-disabled`
4.`ng-checked`
5.`ng-readonly`
6.`ng-selected`
7.`ng-class`
8.`ng-style`

`ng-disabled` --  `disabled` 属性

```html
    <textarea ng-disabled="isDisabled">Wait5seconds</textarea>
```

```javascript
angular.module('myApp', []).run(function($rootScope, $timeout) {
    $rootScope.isDisabled = true;
    $timeout(function() {
        $rootScope.isDisabled = false;
    }, 5000);
})
```

`ng-readonly` -- `readonly` 属性 和 `ng-disabled` 同理

`ng-checked` -- `checked` 属性

```html
    <label>someProperty = {{someProperty}}</label>
    <input type="checkbox"
            ng-checked="someProperty"
            ng-init="someProperty = true"
            ng-model="someProperty">
```

`ng-href` `ng-src` -- 属性动态创建URL/src

逻辑指令
`ng-include`
`ng-switch`
`ng-repeat`
`ng-view`
`ng-controller`
`ng-if`

`ng-include` -- 加载、编译并包含外部HTML片段到当前的应用中
```html
<div ng-include="/myTemplateName.html"
        ng-controller="MyController"
        ng-init="name = 'World'">
        Hello {{ name }}
</div>
```

`ng-if` -- 根据表达式的值在DOM中生成或移除一个元素
ng-if 同 no-show 和 ng-hide 指令最本质的区别是，它不是通过CSS显示或隐藏DOM节点，而
是真正生成或移除节点。

`ng-repeat` -- 遍历一个集合或为集合中的每个元素生成一个模板实例

```html
<li ng-repeat="person in people" ng-class="{even: !$even, odd: !$odd}">
    {{person.name}} lives in {{person.city}}
</li>
```
特殊的属性
`$index` ：遍历的进度（0... length-1 ）。
`$first` ：当元素是遍历的第一个时值为 `true` 。
`$middle` ：当元素处于第一个和最后元素之间时值为 `true` 。
`$last` ：当元素是遍历的最后一个时值为 `true` 。
`$even` ：当 `$index` 值是偶数时值为 `true` 。
`$odd` ：当 `$index` 值是奇数时值为 `true` 。

`ng-init` -- 指令被调用时设置内部作用域的初始状态
```html
<div ng-init="greeting='Hello';person='World'">
    {{greeting}} {{person}}
</div>
```

`ng-bind` 通过 ng-bind指令实现`{{ name }}`的行为
```html
<body ng-init="greeting='HelloWorld'">
    <p ng-bind="greeting"></p>
</body>
```

`ng-model` -- 将 input 、 select 、 text area 或自定义表单控件同包含它们的作用域中的属性进行绑定
```html
<input type="text" ng-model="modelName.someProperty" />
```

`ng-show`/`ng-hide`  -- 根据所给表达式的值来显示或隐藏HTML元素

`ng-change` -- 在表单输入发生变化时计算给定表达式的值,要和 `ng-model` 联合起来使用

`ng-click` -- 指定一个元素被点击时调用的方法或表达式
```html
<button ng-click="count = count + 1" ng-init="count=0"> Increment </button>
<button ng-click="decrement()">Decrement</button>
```
```javascript
angular.module('myApp', []).controller('CounterController', function($scope) {
    $scope.decrement = function() {
        $scope.count = $scope.count - 1;
    };
})
```

`ng-class` -- 动态设置元素的类
```html
<div ng-class="{red: x > 5}"
        ng-if="x > 5">
        You won!
</div>
```