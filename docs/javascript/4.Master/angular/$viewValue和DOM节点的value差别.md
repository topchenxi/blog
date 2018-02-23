### [分析] angular directive中 $viewValue和DOM节点的value 差别

工作上经常遇到dom赋值后发现model没变，或者model赋值后dom没变
所以写个dome来记录下原因

> html

```html

<div class="p20">
    <p>input的model值: {{testValue}}</p>
    <p>实际input展现出来的值:
        <input ngc-model-test type="text" ng-model="testValue" class="input-cfec">
    </p>
</div>

```

> js

```js

    var ngUM = angular.module('ngc.umeditor', []);

    ngUM.directive('ngcModelTest', function() {
        return {
            restrict: 'A',
            require: '?ngModel',
            scope: {
                ngModel: '=',
            },
            link: function(scope, element, attr, ngModel) {

                // 获取model值 ngModel.$viewValue
                // 设置model值 ngModel.$setViewValue('')

                // 获取dom值 element.val()
                // 设置dom值 element.val('')

                element.on('click', function(event) {
                    // action1();
                    // action2();
                    // action3();
                    // action4();
                    // action5();
                });

                function action1() {
                    element.val('1');
                    // 结果 
                    // input的model值: test
                    // 实际input展现出来的值: 1
                    // 结论
                    // 不仅model值没有变化，ngModel的$viewValue和$modelValue同样也没有变化
                    // input的value值不一定等于$viewValue
                }

                function action2() {
                    ngModel.$setViewValue('2');
                    // 结果 
                    // input的model值: 2
                    // 实际input展现出来的值: test
                    // 结论
                    // 执行完$setViewValue之后，无论是viewValue和modelValue都是已经同步了，
                    // 但是input里面的值却依然是test
                    // $viewValue和DOM节点的value是不同的
                }

                function action3() {
                    element.val('3');
                    ngModel.$render();
                    // 结果 
                    // input的model值: test
                    // 实际input展现出来的值: test
                    // 结论
                    // 通过dom赋值了3 ，但没有改变model 所以model的值还是 test
                    // 但是 $render 又把 model 重新赋值搭配 dom 里面
                    // 所以input里面的值却依然是test
                }

                function action4() {
                    ngModel.$setViewValue('4');
                    ngModel.$render();
                    // 结果 
                    // input的model值: 4
                    // 实际input展现出来的值: 4
                    // 结论
                    // 通过model赋值了 4  ，然后把model的值通过 $render() 赋值到dom里面
                    // 所以input里面的值为 4
                }

                // 看看 $render的源码
                /*
                    ngModel.$render = function() {
                        var value = ngModel.$isEmpty(ngModel.$viewValue) ? '' : ngModel.$viewValue;
                        element.val(value);
                    };
                */
                // 本质就是把 model 的值同步到 dom里面

                // 最后 正确的同步赋值如下
                // dom => model
                function setModelValue() {
                    var val = element.val();
                    ngModel.$setViewValue(val);
                }

                function action5() {
                    element.val('5');
                    scope.$apply(setModelValue);
                    // 把dom 的值同步到 model 里面
                }

                // model => dom

                // 一般都是重写 $render，不如以前编辑器里面的同步
                /*
                    ngModel.$render = function() {
                        _initContent = (ctrl.$isEmpty(ctrl.$viewValue) ? "" : ctrl.$viewValue);
                        // 拿到model进行dom赋值操作
                        if (_initContent && editor && _editorReady) {
                            editor.setContent(_initContent);
                        }
                    };
                */

            }
        }
    })
    
```

