# vue 脱坑记

不限于但包括 vue 的问题汇总 ，还有些一些微信群常问的问题

## 安装超时

`cnpm` : 国内对npm的镜像版本
```
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

`yarn` 和 `npm` 改源大法
```
使用 nrm 模块 : www.npmjs.com/package/nrm
npm config : npm config set registry https://registry.npm.taobao.org
yarn config : yarn config set registry https://registry.npm.taobao.org
```

## 安装一些需要编译的包:提示没有安装python、build失败等

window 用户依赖 visual studio 的一些库和python 2+,

[windows-build-tools](https://github.com/felixrieseberg/windows-build-tools)

[python](https://www.python.org/downloads/)

## can't not find 'xxModule'

找不到某些依赖或者模块

缺什么 install 什么 或者 重新安装(windows)
```bash
rmdir /s/q node_modules
cnpm install
```

## 组件内的原生控件添加事件,怎么不生效

错误写法
```html
<!-- 1 -->
<el-input placeholder="请输入特定消费金额 " @mouseover="test()"></el-input>
<!-- 2 -->
<router-link :to="item.menuUrl" @click="toggleName=''">
  <i :class="['fzicon',item.menuIcon]"></i>
  <span>{{item.menuName}}</span>
</router-link>
```
上面的两个例子都没法触发事件 其原因,少了一个修饰符 .native
正确写法
```html
<router-link :to="item.menuUrl" @click.native="toggleName=''">
  <i :class="['fzicon',item.menuIcon]"></i>
  <span>{{item.menuName}}</span>
</router-link>
```

## axios 兼容 ie

IE 整个家族都不支持 promise

`解决方案`
```bash
npm install es6-promise
```
在 main.js 引入即可
```js
require("es6-promise").polyfill();
```

## @click.prevent , v-demo.a.b

`@click.prevent `: 事件+修饰符 , 作用就是点击但又阻止默认行为

`v-demo.a.b`: 自定义指令+修饰符. 具体看你什么指令了,修饰符的作用大多是给事件增加一些确切的拓展功能

详情请看
[事件修饰符](https://cn.vuejs.org/v2/guide/events.html#事件修饰符)

## 图片渲染出来却是 data:image/png;base64xxxxxxxx

这个是 `webpack` 里面的对应插件处理的.

对于小于多少k 以下的图片(规定的格式)直接转为 `base64`格式渲染;

具体配置在`webpack.base.conf.js`里面的 `rules` 里面的 `url-loader`

这样做的好处:在网速不好的时候先于内容加载和减少http的请求次数来减少网站服务器的负担。

## Component template shold contain exactly one root element.If you are useing v-if on multiple elements , xxxxx

单组件渲染 DOM 区域必须要有一个根元素,不能出现同级元素(唯一的父类)

`解决方案`
一个 div(父包含块) 内部多少个同级或者嵌套都行,但是最外层元素不能出现同级元素

## 跨域问题

-`CORS` : 前后端都要对应去配置,IE10+

-`nginx` : 反向代理

`vue-cli`:

在 config 目录下的index.js
```js
proxyTable: {
    "/bp-api": {
        target: "http://new.d.st.cn",
        changeOrigin: true,
        pathRewrite: {
          "^/xxx": "/"
        }
    }
}
```
-`target`: 就是 api 的代理的实际路径

-`changeOrigin`: 就是是变源,(必须 `true` )

-`pathRewrite`: 就是路径重定向,一看就知道

## 数组值更新
[数组更新检测](https://cn.vuejs.org/v2/guide/list.html#数组更新检测) 了解一下

## 为什么组件间的样式不能继承或者覆写

单组件开发模式下,请确认是否开启了 CSS模块化功能!!

也就是`scoped` ( `vue-cli` 里面配置了,只要加入这个属性就自动启用 )

```html
<style lang="scss" scoped>
</style>
```
为什么不能继承或者覆写呢,那时因为每个类或者 id 乃至标签都会给自动在css后面添加hash!
比如

```css
/* 写的时候是这个 */
.trangle{}
/* 编译过后,加上了 hash */
.trangle[data-v-1ec35ffc]{}
```
这些都是在 `css-loader` 里面配置!!!

## 路由模式改为history后,除了首次启动首页没报错,刷新访问路由都报错!

必须给对应的服务端配置查询的主页面..也可以认为是主路由入口的引导

就是 `nginx` 遇到404页面时指向 `index.html`

[HTML5 History 模式](https://router.vuejs.org/zh-cn/essentials/history-mode.html) 了解一下

## npm run build之后不能直接访问

部署本地服务器 如 ： `http-server`

## CSS background 引入图片打包后,访问路径错误

因为打包后图片是在根目录下,你用相对路径肯定报错啊....

你可以魔改 `webpack` 的配置文件里面的`static`为`./static`(不建议)

你若是把图片什么丢到`assets`目录下,然后相对路径,打包后是正常的

## axios 的 post
```bash
npm install qs -S
```
```js
/*
然后在对应的地方转就行了..单一请求也行,拦截器也行...我是写在拦截器的.
具体可以看看我 axios 封装那篇文章
POST传参序列化(添加请求拦截器)
*/
Axios.interceptors.request.use(
    config => {
        // 在发送请求之前做某件事
        if (config.method === "post") { // 序列化
            config.data = qs.stringify(config.data); // ***** 这里转义
        }
        // 若是有做鉴权token , 就给头部带上token
        if (localStorage.token) {
            config.headers.Authorization = localStorage.token;
        }
        return config;
    },
    error => {
        Message({
            //  饿了么的消息弹窗组件,类似toast
            showClose: true,
            message: error,
            type: "error.data.error.message"
        });
        return Promise.reject(error.data.error.message);
    }
);
```

## flex布局错乱!

`autoprefixer` 了解一下

## Vue 网站为什么 UC 访问一片空白

有一种情况绝对会造成,那就是 `ES6` 的代码降级不够彻底. 其他情况可能就是路由配置问题(自己去排除)

现在的开发都推荐按需引入,靠`babel-preset-env` 来控制,以达到打包体积减小.(不兼容老浏览器)

所以最好把代码完全 ES5 话!!记住有些特性不能乱使用,没有对应的 `polyfill`,比如 ES6 的`proxy`

## 既然localStorage和sessionStorage能做到数据维护,为什么还要引入vuex

Vuex的目的用来维护同级组件间的数据通讯,拥有一个共同的状态树

`使用原因` :

可维护性: 因为是单向数据流,所有状态是有迹可循的...数据的传递也可以及时分发响应

易用性: 它使得我们组件间的通讯变得更强大,而不用借助中间件这类来实现不同组件间的通讯

`使用范围` :

涉及需要维护的数据比较多,同级组件间的通讯比较频繁

## vuex的用户信息为什么还要存一遍在浏览器里(sessionStorage or localStorage)

因为 vuex的 store 干不过刷新啊.

保存在浏览器的缓存内,若用户刷新的话,数据重新获取

## 单组件中里面的 import xxx from '@/components/layout/xxx'中的@是什么

`别名机制`

build -> webpack.base.conf.js

```js
 resolve: {
 	extensions: [".js", ".vue", ".json"], // 可以导入的时候忽略的拓展名范围
 	alias: {
 		"@": resolve("src"), // 这里就是别名了
 		"components": resolve("src/components")
 	}
 },
```

## 为什么我的 npm 或者 yarn 安装依赖会生成 lock文件,有什么用
```
lock 文件的作用是统一版本号,这对团队协作有很大的作用;

若是没有 lock 锁定,根据package.json里面的^,~这些..

不同人,不同时间安装出来的版本号不一定一致;
```

## 组件可以缓存么

`keep-alive` 

## 首屏加载比较慢

-减少第三方库的使用,比如jquey这些都可以不要了,很少操作 dom,而且原生基本满足开发
-若是引入moment这些,webpack 排除国际化语言包
-webpack 常规压缩js,css, 愿意折腾的还可以引入 dll 这些
-路由组件采用懒加载
-加入路由过渡和加载等待效果

## Vue SPA 没法做优化(SEO)

可以的,SSR(服务端渲染就能满足你的需求),因为请求回来就是一个处理完毕的 html

[nuxtjs](https://zh.nuxtjs.org/) 了解一下

## Vue 可以写桌面端么

有`electron`和`node-webkit(nw)`

[electronjs](https://electronjs.org/)

[electron-vue](https://github.com/SimulatedGREG/electron-vue)

## Vue写微信小程序

[wepy](https://tencent.github.io/wepy/)

[mpvue](http://mpvue.com/)

## mock 数据

[easy-mock](https://github.com/easy-mock/easy-mock)

[Mock](https://github.com/nuysoft/Mock)
