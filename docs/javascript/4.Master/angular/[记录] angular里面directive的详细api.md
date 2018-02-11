### angular里面directive的api，工作上常用，记录下来，方便用的时候查询

```js

    var ngMyDir = angular.module('myApp', []);


    ngMyDir.directive('myDirective', function() {
        return {
            /*
                restrict: 指明指令在DOM里面以什么形式被声明
                E(元素) ：<myDirective></myDirective>
                A(属性) ：<div myDirective='expression'></div>
                C(类)   ：<div class='myDirective'></div>
                M(注释) ：<--directive:myDirective expression-->
            */
            restrict: 'A',
            /*
                指令的优先级，若在单个DOM上有多个指令，则优先级高的先执行
            */
            priority: 500,
            /*            
                true或false，若设置为true，则优先级低于此指令的其他指令则无效，不会被调用(优先级相同的还是会执行)
                告诉AngularJS停止运行当前元素上比本指令优先级低的指令
             */
            // terminal: true, 
            /*
                插入模版
                1: HTML文本
                2: 函数，可接受两个参数tElement和tAttrs
            */
            // template: '<a href="http://google.com">Click me to go to Google < /a>'
            template: function(element, attr) {
                // console.log(element);
                // console.log($(element).text());
                return '<p style="background-color:{{color}}">Hello World</p>';
            },
            /*
                templateUrl:异步加载模版
                <script type='text/ng-template' id='woshimuban.html'>
                    <div>我是模板内容</div>
                </script>
            */
            // templateUrl: 'template.html',
            /*
                渲染出来的HTML有没有带定义的标签 false时带出自定义标签
            */
            replace: true,
            /*
                为标识符创建一个新的作用域吗，而不是继承父父的作用域
                false:(继承不隔离) 父作用域和子作用域 scope共用（默认）
                true:(继承不隔离) 父作用域和子作用域 scope共用 ，但是子作用域的值改变，父作用域不变
                {}:（不继承隔离）没有继承父作用域的值，所以子作用域，改变任何一方的值均不能影响另一方的值，
                    但是可以用过  <div my-directive color-attr="{{testVm.name}}"></div> 
                    如果绑定的隔离作用域属性名与元素的属性名相同，则可以采取缺省写法 '@'
                    还可以 使用=（=attr）进行双向绑定 <div my-directive color="testVm.name"></div>
                    传递函数用& <div my-directive saysomething999="say();"></div> 
            */
            scope: {
                color: '@colorAttr',
                // color: '=',
                // saysomething:'&saysomething999',
            },
            // 定义 控制器 可以 controller: 'SomeController'  也可以匿名，如下
            controller: function($scope, $element, $attrs, $transclude, $log) {
                // $scope，与指令元素相关联的作用域
                // $element，当前指令对应的 元素
                // $attrs，由当前元素的属性组成的对象
                // $transclude，嵌入链接函数，实际被执行用来克隆元素和操作DOM的函数
                // console.log($scope.color);
                // $scope.color = '#666';
                // console.log($scope.color); // 改变了没用。。
            },
            // 通过标识符拷贝编程修改dom模版  compile 和 link 只能选一种
            // controller先运行，compile后运行，link不运行(link就是compile中的postLink)
            // controller先运行，link后运行，link和compile不兼容
            compile: function(element, attributes) {
                console.log(element.text());
                console.log(element);
                console.log(attributes);
                return {
                    pre: function preLink(scope, iElement, iAttrs, controller) {
                        console.log(1, scope, iElement, iAttrs, controller);
                    },
                    post: function postLink(scope, iElement, iAttrs, controller) {
                        console.log(2, scope, iElement, iAttrs, controller);
                    }
                }
            },
            link: function($scope, $element, $Attributes, $ctrls) {
                // $scope      -- 指令用来在其内部注册监听器的作用域
                // $element -- 实例元素，指使用此指令的元素
                // $Attributes -- 实例属性，是一个由定义在元素上的属性组成的标准化列表，可以在所有指令的链接函数间共享


               // 为了设置作用域中的视图值，需要调用 $ctrls.$setViewValue() 函数
               /*
                    控制器中定义 $render 方法可以定义视图具体的渲染方式
                    ngModel.$render = function() {
                        element.html(ngModel.$viewValue() || 'None');
                    }
               */
            },
            // 第二种方式
            link: {
                // 使用pre-link函数可以运行一些业务代码在ng执行完compile函数之后,
                // 但是在它所有子指令的post-link函数将要执行之前.
                pre: function($scope, $element, $Attributes, $ctrls) {
                    console.log(1);
                },
                // 使用post-link函数来执行业务逻辑,在这个阶段,它已经知道它所有的子指令已经编译完成
                // 并且pre-link以及post-link函数已经执行完成
                post: function($scope, $element, $Attributes, $ctrls) {
                    console.log(2);
                }
            }
        };
    });
```