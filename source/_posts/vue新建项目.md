title: vue新建项目
tags:
  - VUE
author: Mia Liu
categories:
  - 前端
date: 2018-04-25 17:24:00
---
##### 新建VUE项目
环境要求：  安装有 Node.js、 vue、 vue-cli<br/>
###### 在硬盘上找一个文件夹放工程用的，在终端中进入该目录,cd目录路径
npm install -g cnpm --registry=https://registry.npm.taobao.org  // 为了加快速度，不必须

###### 安装webpack 
cnpm install webpack-g
###### 安装vue脚手架
npm install vue-cli-g


然后就可以创建vue项目了

###### 创建项目
* vue init webpack projectName
* Npm install
* Npm run dev

<br/><br/>
###### `一些其他tips`

删除node_modules文件夹
* npm install rimraf -g 
* rimraf node_modules


使用sass
安装sass的依赖包
* npm install --save-dev sass-loader //sass-loader依赖于node-sass 
* npm install --save-dev node-sass


引用sass/scss 文件
* @import "./common/scss/mixin";

<br/><br/>
###### 配置 flexible
* 安装 lib-flexible
	* npm i lib-flexible --save
* 引入 lib-flexible,在项目入口文件 main.js 里 引入 lib-flexible

* 添加 meta 标签
 * 在项目根目录的 index.html 中添加如下 meta
 
```javascript
<meta name="viewport" content="width=device-width, initial-scale=1.0">
```

<br/>
###### px 转 rem
实际开发中，我们通过设计稿得到的值单位是 px，所以要将 px 转换成 rem 再写进样式中。<br/>
将 px 转换成 rem 我们将使用 px2rem 这个工具，它有 webpack 的 loader：px2rem-loader 
* 安装 px2rem-loader
 * npm i px2rem-loade --save-dev
* 配置 px2rem-loade
>在 vue-cli 生成的 webpack 配置中，vue-loader 的 options 和其他样式文件 loader 最终是都是由 build/utils.js 里的一个方法生成的。

我们只需在 cssLoader 后再加上一个 px2remLoader 即可，px2rem-loader 的 remUnit 选项意思是 1rem=多少像素，结合 lib-flexible 的方案，我们将 px2remLoader 的 options.remUnit 设置成设计稿宽度的 1/10，这里我们假设设计稿宽为 750px。
```javascript
	// utils.js
var cssLoader = {
  loader: 'css-loader',
  options: {
    minimize: process.env.NODE_ENV === 'production',
    sourceMap: options.sourceMap
  }
}
var px2remLoader = {
  loader: 'px2rem-loader',
  options: {
    remUnit: 75
  }
}
// ...
```
并放进 loaders 数组中
```javascript
// utils.js
function generateLoaders(loader, loaderOptions) {
  var loaders = [cssLoader, px2remLoader]
// ...
```
修改配置后需要重启，然后我们在组件中写单位直接写 px，设计稿量多少就可以写多少。<br/>
`都是在网上收录的，供自己看`