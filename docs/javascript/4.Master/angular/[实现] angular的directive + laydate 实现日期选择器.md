### [实现] angular的directive + laydate 实现日期选择器

因为最近anguar项目里大量用到日期选择器，每次调用都要初始的话显得麻烦，而且代码很冗余
所以就用angular的directive 来封装下laydate ，调用的时候就很方便了。代码如下：

> 首先先介绍下laydate

[官方首页](https://www.layui.com/laydate/)

全部参数

```
{
  elem: '#id', //需显示日期的元素选择器
  event: 'click', //触发事件
  format: 'YYYY-MM-DD hh:mm:ss', //日期格式
  istime: false, //是否开启时间选择
  isclear: true, //是否显示清空
  istoday: true, //是否显示今天
  issure: true, 是否显示确认
  festival: true //是否显示节日
  min: '1900-01-01 00:00:00', //最小日期
  max: '2099-12-31 23:59:59', //最大日期
  start: '2014-6-15 23:00:00',  //开始日期
  fixed: false, //是否固定在可视区域
  zIndex: 99999999, //css z-index
  choose: function(dates){ //选择好日期的回调
 
  }
}
// 其中 istime,isclear,istoday,issure都使用默认值，要控制的话等需求扩展
```

> HTML部分

```HTML
<div class="form-group">
    <input ngc-my-date type="text" ng-model="startTime" id="startTime" max-date="{{endTime}}" format='YYYY-MM-DD' placeholder="开始日期"/>
    <span class="text-inline">至</span>
    <input ngc-my-date type="text" ng-model="endTime" id="endTime" min-date="{{startTime}}" format='YYYY-MM-DD' placeholder="结束日期"/>
</div>
```

> js部分

```javascript

var ngDate = angular.module('myApp', []);

    ngDate.directive('ngcMyDate', function() {
        return {
            restrict: 'A',
            require: '?ngModel',
            scope: {
                ngModel: '=',
                maxDate: '@',
                minDate: '@'
            },
            link: function(scope, element, attr, ngModel) {
                var _date = null,
                    _config = {};

                if (!attr.id) {
                    element.attr('id', '_laydate' + (Date.now()));
                }
                
                // 日期配置参数
                _config = {
                    elem: '#' + element.attr('id'),
                    format: attr.hasOwnProperty('format') && attr.format ? attr.format : 'YYYY-MM-DD',
                    min: attr.hasOwnProperty('minDate') && attr.minDate ? attr.minDate : '',
                    max: attr.hasOwnProperty('maxDate') && attr.maxDate ? attr.maxDate : '',
                    choose: function(data) {
                        scope.$apply(setDateVal);
                    },
                    clear: function() {
                        ngModel.$setViewValue(null);
                    }
                };
                // 初始化日期
                _date = laydate(_config);

                // 监听 maxDate 变化
                if (attr.hasOwnProperty('maxDate')) {
                    attr.$observe('maxDate', function(val) {
                        _config.max = val;
                    })
                }
                // 监听 minDate 变化
                if (attr.hasOwnProperty('minDate')) {
                    attr.$observe('minDate', function(val) {
                        _config.min = val;
                    })
                }

                // 监听输入框 时刻同步 $viewValue 和 DOM节点的value
                ngModel.$render = function() {
                    element.val(ngModel.$viewValue || '');
                };

                // 监听输入框 时刻同步 $viewValue 和 DOM节点的value
                element.on('blur keyup change', function() {
                    scope.$apply(setDateVal);
                });

                setDateVal();

                // 同步 DOM节点的value 到 $viewValue 
                function setDateVal() {
                    var val = element.val();
                    ngModel.$setViewValue(val);
                }
            }
        }
    })

```


