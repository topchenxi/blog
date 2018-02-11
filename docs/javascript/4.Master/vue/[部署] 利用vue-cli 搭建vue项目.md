### [部署] 利用vue-cli 搭建vue项目

#### Node.js安装

[node](https://nodejs.org/en/download/)

#### 安装vue-cli
```bash
npm install -g vue-cli
```
国内小伙伴可以使用[cnpm](http://npm.taobao.org/)
```bash
npm install -g cnpm --registry=https://registry.npm.taobao.org
```

#### 使用vue-cli初始化项目

```
vue init <template-name> <project-name>
```

Example:
```bash
vue init webpack my-project
```
或
```bash
vue init webpack-simple my-project
```

接着执行命令
```
cd my-project
npm install
```

到目前为止项目文件已经全部安装在本地上了

项目运行就要执行如下：

* `npm run dev`: Webpack + vue-loader with proper config for source maps & hot-reload.

* `npm run build`: build with HTML/CSS/JS minification.



