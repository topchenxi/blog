# vue

## Vue对象
```js
var vm = new Vue({
    // 数据
    data: "声明需要响应式绑定的数据对象",
    props: "接收来自父组件的数据",
    propsData: "创建实例时手动传递props，方便测试props",
    computed: "计算属性",
    methods: "定义可以通过vm对象访问的方法",
    watch: "Vue实例化时会调用$watch()方法遍历watch对象的每个属性",
    // DOM
    el: "将页面上已存在的DOM元素作为Vue实例的挂载目标",
    template: "可以替换挂载元素的字符串模板",
    render: "渲染函数，字符串模板的替代方案",
    renderError: "仅用于开发环境，在render()出现错误时，提供另外的渲染输出",
    // 生命周期钩子
    beforeCreate: "发生在Vue实例初始化之后，data observer和event/watcher事件被配置之前",
    created: "发生在Vue实例初始化以及data observer和event/watcher事件被配置之后",
    beforeMount: "挂载开始之前被调用，此时render()首次被调用",
    mounted: "el被新建的vm.$el替换，并挂载到实例上之后调用",
    beforeUpdate: "数据更新时调用，发生在虚拟DOM重新渲染和打补丁之前",
    updated: "数据更改导致虚拟DOM重新渲染和打补丁之后被调用",
    activated: "keep-alive组件激活时调用",
    deactivated: "keep-alive组件停用时调用",
    beforeDestroy: "实例销毁之前调用，Vue实例依然可用",
    destroyed: "Vue实例销毁后调用，事件监听和子实例全部被移除，释放系统资源",
    // 资源
    directives: "包含Vue实例可用指令的哈希表",
    filters: "包含Vue实例可用过滤器的哈希表",
    components: "包含Vue实例可用组件的哈希表",
    // 组合
    parent: "指定当前实例的父实例，子实例用this.$parent访问父实例，父实例通过$children数组访问子实例",
    mixins: "将属性混入Vue实例对象，并在Vue自身实例对象的属性被调用之前得到执行",
    extends: "用于声明继承另一个组件，从而无需使用Vue.extend，便于扩展单文件组件",
    provide & inject: "2个属性需要一起使用，用来向所有子组件注入依赖，类似于React的Context",
    // 其它
    name: "允许组件递归调用自身，便于调试时显示更加友好的警告信息",
    delimiters: "改变模板字符串的风格，默认为{{}}",
    functional: "让组件无状态(没有data)和无实例(没有this上下文)",
    model: "允许自定义组件使用v-model时定制prop和event",
    inheritAttrs: "默认情况下，父作用域的非props属性绑定会应用在子组件的根元素上。当编写嵌套有其它组件或元素的组件时，可以将该属性设置为false关闭这些默认行为",
    comments: "设为true时会保留并且渲染模板中的HTML注释"
});
```

## 实例属性和方法
```js
let vm = new Vue();
vm = {
    // Vue实例属性的代理
    $data: "被watch的data对象",
    $props: "当前组件收到的props",
    $el: "Vue实例使用的根DOM元素",
    $options: "当前Vue实例的初始化选项",
    $parent: "父组件Vue对象的实例",
    $root: "根组件Vue对象的实例",
    $children: "当前实例的直接子组件",
    $slots: "访问被slot分发的内容",
    $scopedSlots: "访问scoped slots",
    $refs: "包含所有拥有ref注册的子组件",
    $isServer: "判断Vue实例是否运行于服务器",
    $attrs: "包含父作用域中非props的属性绑定",
    $listeners: "包含了父作用域中的v-on事件监听器",
    // 数据
    $watch: "观察Vue实例变化的表达式、计算属性函数",
    $set: "全局Vue.set的别名",
    $delete: "全局Vue.delete的别名",
    // 事件
    $on: "监听当前实例上的自定义事件，事件可以由vm.$emit触发",
    $once: "监听一个自定义事件，触发一次之后就移除监听器",
    $off: "移除自定义事件监听器",
    $emit: "触发当前实例上的事件",
    // 生命周期
    $mount: "手动地挂载一个没有挂载的Vue实例",
    $forceUpdate: "强制Vue实例重新渲染，仅影响实例本身和插入插槽内容的子组件",
    $nextTick: "将回调延迟到下次DOM更新循环之后执行",
    $destroy: "完全销毁一个实例",
}
```

## 双向绑定

`Vue`组件不能检测到实例化后data属性的添加、删除

因为`Vue`组件在实例化时才会对属性执行`getter`/`setter`处理

准确的描述应该是单向绑定，响应式更新

而`Angular`即可以通过`$scope`影响`view`上的数据绑定，也可以通过视图层操作`$scope`上的对象属性，属于真正意义上的`视图与模型的双向绑定`

```js
var vm = new Vue({
    el: "#app",
    data: {
        name: 'c.c.'
    }
})
vm.name = 'saving' // 响应的
vm.title = 'v.v.' // 非响应的
```
Vue不允许在已经实例化的组件上添加新的动态根级响应属性
```js
Vue.set(vm.obj, "b", 2)
// vm.$set()实例方法是Vue.set()全局方法的别名
// 使用Object.assign()或_.extend()也可以添加响应式属性，但是需要创建同时包含原属性、新属性的对象，从而有效触发watch()方法
vm.obj = Object.assign({}, vm.obj, { a: 1, b: 2 })
```

为了在`Vue`响应数据变化之后再更新DOM，可以手动调用`Vue.nextTick(callback)`

并将`DOM操作`逻辑放置在`callback`回调函数中

```js
Vue.name = "saving" // 更改数据
Vue.$el.textContent === "saving" // false 没有更新
Vue.nextTick(function() {
    vm.$el.textContent === "saving" // true // 更新完成
})
```

## mixin
```js
// mixin对象
var mixin = {
    created: function() {
        console.log("混合对象的钩子被调用"); // 先执行
    },
    methods: {
        name: function() {
            console.log("saving")
        }
    }
}
// vue属性
var vm = new Vue({
    el: '#app',
    mixins: [mixin],
    created: function() {
        console.log("组件钩子被调用");
        this.name();
    },
    methods: {
        title: function() {
            console.log("c.c.")
        }
    }
})
```

## render
```js
// vue属性
var vm = new Vue({
    el: '#app',
    data: function() {
        return {
            name: 'saving'
        };
    },
    render: function(createElement) {
        return createElement("h1", this.name)
    }
})
```

## Vue对象全局API
```js
Vue.extend(options)                 // 通过继承一个option对象来创建一个Vue实例。
Vue.nextTick([callback, context])   // 在下次DOM更新循环结束之后执行延迟回调。
Vue.set(target, key, value)         // 设置对象的属性，如果是响应式对象，将会触发视图更新。
Vue.delete(target, key)             // 删除对象的属性，如果是响应式对象，将会触发视图更新。
Vue.directive(id, [definition])     // 注册或获取全局指令。
Vue.filter(id, [definition])        // 注册或获取全局过滤器。
Vue.component(id, [definition])     // 注册或获取全局组件。
Vue.use(plugin)                     // 安装Vue插件。
Vue.mixin(mixin)                    // 全局注册一个mixin对象。
Vue.compile(template)               // 在render函数中编译模板字符串。
Vue.version                         // 提供当前使用Vue的版本号。
```

## Vue.directive
```js
Vue.directive("focus", {
    bind: function() {
        // 指令第一次绑定到元素时调用，只会调用一次，可以用来执行一些初始化操作。
    },
    inserted: function(el) {
        // 被绑定元素插入父节点时调用。
    },
    update: function() {
        // 所在组件的VNode更新时调用，但是可能发生在其子VNode更新之前。
    },
    componentUpdated: function() {
        // 所在组件VNode及其子VNode全部更新时调用。
    },
    unbind: function() {
        // 指令与元素解绑时调用，只会被调用一次。
    }
})
```

## 数据绑定
```html
<h2>{{name}}</h2>
<div>Message: {{ name }}</div>
<section v-once>一次性绑定: {{ name }}</section>
<div v-html="name"></div>
<div :id="id"></div>
<button :disabled="bool">Button</button>
```

## class
```html
<!-- 直接绑定class到一个对象 -->
<div v-bind:class="myClassName">myClassName</div>
<!-- 直接绑定class到对象的属性 -->
<div class="static" v-bind:class="{ active: isActive , current : isCurrent }">isActive</div>
<!-- 绑定class到计算属性 -->
<div v-bind:class="[myClassName, name]"></div>
<!-- 使用三目运算符 -->
<div v-bind:class="[isActive ? 'active' : '', myClassName]"></div>
```

## 内置命令

```html
<html
  v-text = "更新元素的textContent"
  v-html = "更新元素的innerHTML"
  v-show = "根据表达式的true/false，切换HTML元素的display属性"
  v-for = "遍历内部的HTML元素"
  v-pre = "跳过表达式渲染过程，可以显示原始的Mustache标签"
  v-cloak = "保持在HTML元素上直到关联实例结束编译，可以隐藏未编译的Mustache"
  v-once = "只渲染元素和组件一次"
></html>

<!-- 根据表达式的true和false来决定是否渲染元素 -->
<div v-if="type === "A"">A</div>
<div v-else-if="type === "B"">B</div>
<div v-else-if="type === "C"">C</div>
<div v-else>Not A/B/C</div>

<!-- 动态地绑定属性或prop到表达式 -->
<p v-bind:attrOrProp
  .prop = "被用于绑定DOM属性"
  .camel = "将kebab-case特性名转换为camelCase"
  .sync = "语法糖，会扩展成一个更新父组件绑定值的v-on监听器"
></p>
<!-- 绑定事件监听器 -->
<button
  v-on:eventName
  .stop = "调用event.stopPropagation()"
  .prevent = "调用event.preventDefault()"
  .capture = "添加事件监听器时使用capture模式"
  .self = "当事件是从监听器绑定的元素本身触发时才触发回调" 
  .native = "监听组件根元素的原生事件"-
  .once = "只触发一次回调"
  .left = "点击鼠标左键触发"
  .right = "点击鼠标右键触发"
  .middle = "点击鼠标中键触发"
  .passive = "以{passive: true}模式添加监听器"
  .{keyCode | keyAlias} = "触发特定键触事件"
></button>

<!-- 表单控件的响应式绑定 -->
<input 
  v-model
  .lazy = "取代input监听change事件"
  .number = "输入字符串转为数字"
  .trim = "过滤输入的首尾空格" />
```
## 事件

- $on(eventName) 监听事件
- $emit(eventName) 触发事件

.native
根元素上监听原生事件
```html
<my-component v-on:click.native="action"></my-component>
```

.sync
```html
<!-- 使用.sync修饰符 -->
<comp :foo.sync="bar"></comp>
<!-- 被自动扩展为如下形式，该组件的子组件会通过this.$emit("update:foo", newValue)显式触发更新事件 -->
<comp :foo="bar" @update:foo="val => bar = val"></comp>
```

平行组件通信
```js
var bus = new Vue()
// 触发组件A中的事件
bus.$emit("id-selected", 1)
// 在组件B监听事件
bus.$on("id-selected", function(id) {
    // to do
})
```

## CSS作用域

向.vue单文件组件的`<style>`标签上添加scoped属性，可以让该`<style>`标签中的样式只作用于当前组件。

使用scoped时，样式选择器尽量使用class或者id，以提升页面渲染性能。

## 过渡
```html
<transition name="fade" mode="out-in">
  <button v-if="docState === "saved"" key="saved"> Edit </button>
  <button v-if="docState === "edited"" key="edited"> Save </button>
  <button v-if="docState === "editing"" key="editing"> Cancel </button>
</transition>
```