# [部署] 利用vue-cli 搭建vue项目

## Node.js安装

[node 官网](https://nodejs.org/en/download/)

`npm` 因为墙的原因，国内小伙伴可以使用[cnpm](http://npm.taobao.org/)

```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

## 安装vue-cli
```bash
npm install -g vue-cli
```

## 使用vue-cli初始化项目

```
vue init <template-name> <project-name>
```

`browserify`--全功能的Browserify + vueify，包括热加载，静态检测，单元测试

`browserify-simple-`-一个简易的Browserify + vueify，以便于快速开始。

`webpack`--全功能的Webpack + vueify，包括热加载，静态检测，单元测试

`webpack-simple`--一个简易的Webpack + vueify，以便于快速开始。

`simple` - 单个HTML文件中最简单的Vue设置

## 安装package
```
cd my-project
npm install
```

## 启动

-`npm run dev`: Webpack + vue-loader with proper config for source maps & hot-reload.

-`npm run build`: build with HTML/CSS/JS minification.



