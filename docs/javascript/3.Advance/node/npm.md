# npm

## 安装

[官网](https://nodejs.org/en/download/)

国内镜像，下载package比较快
[cnpm](http://npm.taobao.org/)

安装检后查下
```bash
where node
or
which node

C:\Program Files\nodejs\node.exe
```
```bash
node --version
v8.9.4
```

检查npm

```bash
where npm
or
which npm
C:\Program Files\nodejs\npm

npm -v
5.6.0
```

## 命令

安装信息
```bash
npm config list
```

罗列全局路径下的包
```bash
npm list --global

 // 当前目录
npm list
```

## 安装 package.json
```bash
npm init
```

## 删除本地包
```bash
npm uninstall xxx
```

## 更新包

先检查包是否有更新
```bash
npm outdated
```

更新包
```bash
npm update gulp
```

## 寻找包
```bash
npm search xxx
```

## 重新安装项目依赖
```bash
npm install request
```

## 其他命令

install : common options: [-S|--save|-D|--save-dev|-O|--save-optional] [-E|--save-exact] [--dry-run]

- npm install – 安装包
- npm install -g – 安装包到全局下


- npm un – 删除本地下包
- npm up – 更新包
- npm t – 运行测试
- npm ls – 罗列已经安装包
- npm ll or npm la – 罗列包时显示额外信息