### [基础] angular 过滤器介绍

用法

` HTML`
```html
{{ name | uppercase }}
``` 


` javascript `
```javascript
app.controller('DemoController', ['$scope', '$filter',
    function($scope, $filter) {
        $scope.name = $filter('lowercase')('Ari');
    }
]);
```

过滤器介绍：
`currency` - 数值格式化为货币格式
`date`     - 将日期格式化成需要的格式

```html
{{ today | date:'medium' }} <!-- Aug 09, 2013 12:09:02 PM -->
{{ today | date:'short' }} <!-- 8/9/1312:09PM -->
{{ today | date:'fullDate' }} <!-- Thursday, August 09, 2013 -->
{{ today | date:'longDate' }} <!-- August 09, 2013 -->
{{ today | date:'mediumDate' }}<!-- Aug 09, 2013 -->
{{ today | date:'shortDate' }} <!-- 8/9/13 -->
{{ today | date:'mediumTime' }}<!-- 12:09:02 PM -->
{{ today | date:'shortTime' }} <!-- 12:09 PM -->

<!-- 
    官方解析
    `'yyyy'`: 4 digit representation of year (e.g. AD 1 => 0001, AD 2010 => 2010)
    `'yy'`: 2 digit representation of year, padded (00-99). (e.g. AD 2001 => 01, AD 2010 => 10)
    `'y'`: 1 digit representation of year, e.g. (AD 1 => 1, AD 199 => 199)
    `'MMMM'`: Month in year (January-December)
    `'MMM'`: Month in year (Jan-Dec)
    `'MM'`: Month in year, padded (01-12)
    `'M'`: Month in year (1-12)
    `'LLLL'`: Stand-alone month in year (January-December)
    `'dd'`: Day in month, padded (01-31)
    `'d'`: Day in month (1-31)
    `'EEEE'`: Day in Week,(Sunday-Saturday)
    `'EEE'`: Day in Week, (Sun-Sat)
    `'HH'`: Hour in day, padded (00-23)
    `'H'`: Hour in day (0-23)
    `'hh'`: Hour in AM/PM, padded (01-12)
    `'h'`: Hour in AM/PM, (1-12)
    `'mm'`: Minute in hour, padded (00-59)
    `'m'`: Minute in hour (0-59)
    `'ss'`: Second in minute, padded (00-59)
    `'s'`: Second in minute (0-59)
    `'sss'`: Millisecond in second, padded (000-999)
    `'a'`: AM/PM marker
    `'Z'`: 4 digit (+sign) representation of the timezone offset (-1200-+1200)
    `'ww'`: Week of year, padded (00-53). Week 01 is the week with the first Thursday of the year
    `'w'`: Week of year (0-53). Week 1 is the week with the first Thursday of the year
    `'G'`, `'GG'`, `'GGG'`: The abbreviated form of the era string (e.g. 'AD')
    `'GGGG'`: The long form of the era string (e.g. 'Anno Domini')
-->
```

`json` -- 将一个JSON或JavaScript对象转换成字符串
```html
<!-- {{ {'name': 'Ari', 'City': 'SanFrancisco'} | json }}  -->
<!-- {"name": "Ari", "City": "San Francisco"} -->
```

`limitTo` -- 根据传入的参数生成一个新的数组或字符串
```html
{{ San Francisco is very cloudy | limitTo:3 }}
<!-- San -->
{{ San Francisco is very cloudy | limitTo:-6 }}
<!-- cloudy -->
{{ ['a','b','c','d','e','f'] | limitTo:1 }}
<!-- ["a"] -->
```

`lowercase` -- 字符串转为小写
```html
{{ "San Francisco is very cloudy" | lowercase }}
<!-- san francisco is very cloudy -->
```

`uppercase` -- 字符串转换为大写
```html
{{ "San Francisco is very cloudy" | uppercase }}
<!-- SAN FRANCISCO IS VERY CLOUDY -->
```


`number` -- 将数字格式化成文本
```html
{{ 123456789 | number }}
<!-- 1,234,567,890 -->
```

`orderBy` -- 用表达式对指定的数组进行排序
```html
{{ 
    [{'name': 'Ari', 'status': 'awake'},
    {'name': 'Q', 'status': 'sleeping'},
    {'name': 'Nate', 'status': 'awake'}] | orderBy:'name' 
}} 
<!-- [{"name":"Ari","status":"awake"}, {"name":"Nate","status":"awake"}, {"name":"Q","status":"sleeping"} ] -->
```

