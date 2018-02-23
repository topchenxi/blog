
```javascript

    // jquery select 的增删查改
    // 记录一些方法，方便以后自己用的时候查询


    // 1.增
    // 为select 队尾添加一个option
    $("#id").append("<option value='1'>Content</option>");

    // 为select 队首添加一个option
    $("#id").prepend("<option value='0'>All</option>");



    // 2.删
    // 清空 select 所有option
    $("#_id").empty();

    // 删除 select 中索引值最大 option (最后一个)
    $("#id option:last").remove();

    // 删除 select 中索引值最小 option (第一个)
    $("#id option:first").remove();

    // 删除 select 中索引值为0的 option (第一个)
    $("#id option[index='0']").remove();

    // 删除 select 中Value='2'的 option
    $("#id option[value='2']").remove();

    // 删除 select 中Text='3'的Optiona
    $("#id option[text='3']").remove();



    // 3.查
    $("#id").change(function() {
        // 获取 select 选择的text
        console.log('text:', $("#id").find("option:selected").text());
        // 获取 select 选择的Value
        console.log('value:', $("#id").val());
        // 获取 select 选择的索引值
        console.log('index:', $("#id").get(0).selectedIndex);
        // 获取 select 最大的索引值
        console.log('maxIndex:', $('#id option').index($("#id option:last")));
    })

    // 4.改
    // 设置value为3的项选中
    $("#id").val("3");
    // 设置text为4的项选中 不同版本的jquery 兼容性比较差（可以采用循环数组来实现）
    $("#id").find("option[text='4']").attr("selected", 'selected');


```
