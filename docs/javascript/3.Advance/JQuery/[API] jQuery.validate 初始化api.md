# jQuery.validate

## html

```html
<form action="" id="formId">
	<div class="mb20">
		<input type="" name="inputName" id="inputId"></div>
	<div class="mb20">
		<select name="selectName" id="selectId">
			<option value="">All</option>
			<option value="1">1</option>
			<option value="2">2</option>
		</select>
	</div>
	<div class="mb20">
		<label for="checkboxName">
			<input type="checkbox" name="checkboxName" id="checkboxId">单选框</label>
	</div>
	<div class="mb20">
		<input type="text" name="groupName1" id="groupName1">
		<input type="text" name="groupName2" id="groupName2"></div>
	<div class="mb20">
		<button type="button" class="btn formSubmit">提交</button>
	</div>
</form>

```

## validate构建

```javascript
var formValid = $('#formId').validate({
    // 指定错误提示的css类名,可以自定义错误提示的样式
    errorClass: "error-explain",
    // 指定成功提示的css类名,可以自定义错误提示的样式
    validClass: "valid-explain",
    // 指定成功提示的css类名,可以自定义错误提示的样式
    success: "valid-success",
    // 使用什么标签标记错误
    errorElement: "div",
    // 使用什么标签errorELement包起来
    wrapper: "div",
    // 对某些元素不进行验证
    ignore: ":hidden",
    // 是否提交时验证
    onsubmit: true,
    // 是否在获得焦点时验证
    onfocusin: true,
    // 是否在获取焦点时验证
    onfocusout: true,
    // 是否在敲击键盘时验证
    onkeyup: true,
    // 是否在鼠标点击时验证
    onclick: true,
    // 提交表单后,未通过验证的表单(第一个或提交之前获得焦点的未通过验证的表单)会获得焦点
    focusInvalid: true,
    // 当未通过验证的元素获得焦点时,并移除错误提示（避免和 focusInvalid.一起使用
    focusCleanup: false,
    // 对一组元素的验证,用一个错误提示
    groups: {
        group1: 'groupName1 groupName2'
    },
    // 自定义错误放到哪里
    errorPlacement: function(error, element) {
        // 同个父集
        error.appendTo(element.parent());
    },
    rules: {
        inputName: {
            required: true
        },
        selectName: {
            required: true
        },
        checkboxName: {
            required: true
        },
        groupName1: {
            required: true
        },
        groupName2: {
            required: true
        },
        testName: {
            required: true,
            remote: {
                // 后台处理程序
                url: "check-email.php",
                // 数据发送方式
                type: "post",
                // 接受数据格式
                dataType: "json",
                // 要传递的数据
                // 远程地址只能输出 "true" 或 "false"
                data: {
                    testName: function() {
                        return $("#testName").val();
                    }
                }
            },
            email: true,
            url: true,
            date: true,
            dateISO: true,
            number: true,
            digits: true,
            creditcard: true,
            equalTo: "#testName",
            maxlength: 10,
            minlength: 1,
            rangelength: [1, 10],
            range: [1, 10],
            max: 1,
            min: 10,
            remoteMsg: {
                url: '/commonapi/check/checkSensitiveWords.cf'
            }
        }
    },
    messages: {
        inputName: {
            required: '必填项'
        },
        selectName: {
            required: '必填项'
        },
        checkboxName: {
            required: '必填项'
        },
        groupName1: {
            required: '必填项'
        },
        groupName2: {
            required: '必填项'
        },
        testName: {
            required: "必须填写",
            remote: "请修正此栏位",
            email: "请输入有效的电子邮件",
            url: "请输入有效的网址",
            date: "请输入有效的日期",
            dateISO: "请输入有效的日期 (YYYY-MM-DD)",
            number: "请输入正确的数字",
            digits: "只可输入数字",
            creditcard: "请输入有效的信用卡号码",
            equalTo: "你的输入不相同",
            extension: "请输入有效的后缀",
            maxlength: $.validator.format("最多 {0} 个字"),
            minlength: $.validator.format("最少 {0} 个字"),
            rangelength: $.validator.format("请输入长度为 {0} 至 {1} 之間的字串"),
            range: $.validator.format("请输入 {0} 至 {1} 之间的数值"),
            max: $.validator.format("请输入不大于 {0} 的数值"),
            min: $.validator.format("请输入不小于 {0} 的数值"),
            remoteMsg: '不能存在[0]'
        }
    }
})
$('.formSubmit').click(function(event) {
    // 把前面验证的FORM恢复到验证前原来的状态(即清楚错误状态)
    formValid.resetForm();
    console.log(formValid.form());
    console.log(formValid);
    console.log(formValid.invalid);
    console.log(formValid.successList);
    console.log(formValid.errorList);
    // 触发单个输入验证
    $('input[name="inputName"]').valid();
});
```

## addMethod
```js
/*
    addMethod(name,method,message)
    参数 name 是添加的方法的名字。
    参数 method 是一个函数，接收三个参数 (value,element,param) 。
    value 是元素的值，element 是元素本身，param 是参数。
*/
$.validator.addMethod("methodName", function(value, element) {
    var reg;
    // 数值
    // 整数
    reg = /^-?[1-9]\d*$/;
    // 正整数+0
    reg = /^[1-9]\d*|0$/;
    // 正浮点数
    reg = /^[1-9]\d*\.\d*|0\.\d*[1-9]\d*$/;
    // 判断浮点型
    reg = /^[-\+]?\d+(\.\d+)?$/;
    // 只能输入[0-9]数字
    reg = /^\d+$/;
    // 号码
    // 匹配qq
    reg = /[1-9][0-9]{4,}/;
    // 手机号码验证
    // return this.optional(element) || (length == 11 && reg.test(value));
    reg = /^(((13[0-9]{1})|(15[0-9]{1})|(18[0-9]{1}))+\d{8})$/;
    // 电话号码验证
    reg = /^(\d{3,4}-?)?\d{7,9}$/g;
    // 中国邮政编码
    reg = /[1-9]\d{5}(?!\d)/;
    // 美国邮政编码
    reg = /^\d{5}(-\d{4})?$/;
    // 身份证号码验证
    reg = /^(\d{6})(\d{4})(\d{2})(\d{2})(\d{3})([0-9]|X)$/;
    // ipv4
    reg = /^(25[0-5]|2[0-4]\d|[01]?\d\d?)\.(25[0-5]|2[0-4]\d|[01]?\d\d?)\.(25[0-5]|2[0-4]\d|[01]?\d\d?)\.(25[0-5]|2[0-4]\d|[01]?\d\d?)$/i;
    // 字体
    // 判断英文字符
    reg = /^[A-Za-z]+$/;
    // 字符验证，只能包含中文、英文、数字、下划线等字符。
    reg = /^[a-zA-Z0-9\u4e00-\u9fa5-_]+$/;
    // 匹配汉字
    reg = /^[\u4e00-\u9fa5]+$/;
    // 匹配中文(包括汉字和字符)
    reg = /^[\u0391-\uFFE5]+$/;
    // 判断是否为合法字符(a-zA-Z0-9-_)
    reg = /^[A-Za-z0-9_-]+$/;
    // 判断是否包含中英文特殊字符，除英文"-_"字符外
    reg = RegExp(/[(\ )(\`)(\~)(\!)(\@)(\#)(\$)(\%)(\^)(\&)(\*)(\()(\))(\+)(\=)(\|)(\{)(\})(\')(\:)(\;)(\')(',)(\[)(\])(\.)(\<)(\>)(\/)(\?)(\~)(\！)(\@)(\#)(\￥)(\%)(\…)(\&)(\*)(\（)(\）)(\—)(\+)(\|)(\{)(\})(\【)(\】)(\‘)(\；)(\：)(\”)(\“)(\’)(\。)(\，)(\、)(\？)]+/);
    // 数字英文及符号[包含空格],除"<>"外的英文字符
    reg = /^[\w\s`~!@#$%^&*()_+\-=[\]{}\\|;':"/,.?]*$/ig;
    return this.optional(element) || reg.test(value);
}, "errorMesaageTips");

```


###### 官方 api [https://jqueryvalidation.org/](https://jqueryvalidation.org/)
###### runoob api [http://www.runoob.com/jquery/jquery-plugin-validate.html](http://www.runoob.com/jquery/jquery-plugin-validate.html)
