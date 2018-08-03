---
title: "Webpack开发指南教程_学习笔记"
date: 2018-07-26T00:00:06+08:00
draft: true
---

# Webpack开发指南教程：
D:\MyData\Sources\学习网站DownLoad\webpack 中文网https://www.webpackjs.com/guides/
D:\MyData\Learning\Webpack\Webpack_Demo_zhinan_Start
D:\MyData\Learning\Webpack\Webpack_Demo_zhinan_ManageSource

一、起步
1.基本安装
首先我们创建一个目录，初始化 npm，然后在本地安装 webpack，接着安装 webpack-cli（此工具用于在命令行中运行 webpack）
mkdir webpack-demo && cd webpack-demo
npm init -y
npm install webpack webpack-cli --save-dev

创建以下目录结构、文件和内容
webpack-demo
  |- package.json
+ |- index.html
+ |- /src
+   |- index.js

调整 package.json 文件，以便确保我们安装包是私有的(private)，并且移除 main 入口。这可以防止意外发布你的代码。
<script> 标签之间存在隐式依赖关系。index.js 文件执行之前，还依赖于页面中引入的 lodash。之所以说是隐式的是因为 index.js 并未显式声明需要引入 lodash，只是假定推测已经存在一个全局变量 _ 。

2.创建一个 bundle 文件
要在 index.js 中打包 lodash 依赖，我们需要在本地安装 library：
npm install --save lodash

在安装一个要打包到生产环境的安装包时，你应该使用 npm install --save，如果你在安装一个用于开发环境的安装包（例如，linter, 测试库等），你应该使用 npm install --save-dev。

在我们的脚本 src/index.js 中 import lodash：
import _ from 'lodash';

3.使用一个配置文件：webpack.config.js
文件内容如下：
const path = require('path');
module.exports = {
  entry: './src/index.js',
  output: {
    filename: 'bundle.js',
    path: path.resolve(__dirname, 'dist')
  }};

4.命令简化：package.json

"scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "build": "webpack --config webpack.config.js"
    },
运行以下命令，然后看看你的脚本别名是否正常运行：npm run build

二、管理资源
1.安装:修改title为——<title>Asset Management</title>
2.加载CSS：
在 module 配置中安装并添加 style-loader 和 css-loader：
npm install --save-dev style-loader css-loader

再配置webpack.config.js文件：（置于module.exports中）
module: {
    rules: [{
        test: /\.css$/,
        use: [
'            style-loader',
            'css-loader'
        ]
    }]
}

在项目中添加一个新的 style.css 文件，并将其导入到我们的 index.js 中，运行构建命令 npm run build查看效果；

3.加载图片
背景和图标这些图片使用 file-loader，我们可以轻松地将这些内容混合到 CSS中，在 module 配置中安装并添加 file-loader：
npm install --save-dev file-loader

再配置webpack.config.js文件：（置于module.exports中）
{
    test: /\.(png|svg|jpg|gif)$/,
    use: [
        'file-loader'
    ]
}

在项目中添加一个图像icon.png，并将其导入到我们的 index.js 中,在css中设置背景图片，或者在页面中加入图片，运行构建命令npm run build查看效果；
background: url('./icon.png');
或者：
//将图像添加到我们现有的 div。
   var myIcon = new Image();
   myIcon.src = Icon;
   element.appendChild(myIcon);

4.加载字体（略）

5.加载数据
加载的有用资源还有数据，如 JSON 文件，CSV、TSV 和 XML。类似于 NodeJS，JSON 支持实际上是内置的，也就是说 import Data from './data.json' 默认将正常运行。要导入 CSV、TSV 和 XML，你可以使用 csv-loader 和 xml-loader,在 module 配置中安装并添加loader 和 xml-loader:
npm install --save-dev csv-loader xml-loader

再配置webpack.config.js文件：（置于module.exports中）
{
    test: /\.(csv|tsv)$/,
    use: [
    'csv-loader'
    ]
},
{
    test: /\.xml$/,
    use: [
        'xml-loader'
    ]
}
在项目中添加一个文件data.xml，并将其导入到我们的 index.js 中,在页面中加入，运行构建命令npm run build查看效果；
import Data from './data.xml';
console.log(Data);

6.补充： CSS 处理器风格 - postcss, sass 和 less 等
（1）sass转css
在 module 配置中安装并添加 sass-loader 和 node-sass:
npm install sass-loader node-sass --save-dev

再配置webpack.config.js文件：（置于module.exports的module中）
{
    test: /\.scss$/,
    use: [{
    loader: "style-loader" // 将 JS 字符串生成为 style 节点
    }, {
        loader: "css-loader" // 将 CSS 转化成 CommonJS 模块
    }, {
        loader: "sass-loader" // 将 Sass 编译成 CSS
    }]
}

在项目中添加一个文件。。。


（2）less转css
在 module 配置中安装并添加 sass-loader 和 node-sass:
npm install --save-dev less-loader less

再配置webpack.config.js文件：（置于module.exports的module中）
 {
    test: /\.less$/,
    use: [{
        loader: "style-loader" // creates style nodes from JS strings
    }, {
        loader: "css-loader" // translates CSS into CommonJS
    }, {
        loader: "less-loader" // compiles Less to CSS
    }]
}

在项目中添加一个文件。。。


三、管理输出
1.预先准备
先在项目中src文件夹下添加一个文件 print.js， 并添加一些逻辑；
例：export default function printMe() { console.log('I get called from print.js!');}

再在 src/index.js 文件中引入并使用这个函数：
import printMe from './print.js';

var btn = document.createElement('button');
btn.innerHTML = 'Click me and check the console!';
btn.onclick = printMe;
element.appendChild(btn);

再更新 dist/index.html 文件，来为 webpack 分离入口做好准备：
<script src="./print.bundle.js"></script>
<script src="./app.bundle.js"></script>

再配置webpack.config.js文件：（置于module.exports中）
entry: {
    app:'./src/index.js',
    print:'./src/print.js'
},
output: {
    filename: '[name].bundle.js',
    path: path.resolve(__dirname, 'dist')
}

运行构建命令npm run build查看效果，将会在dist文件夹中生成app.bundle.js 和print.bundle.js 两个文件；

2.设定 HtmlWebpackPlugin
首先安装html-webpack-plugin插件，并且调整 webpack.config.js 文件:
npm install --save-dev html-webpack-plugin

配置webpack.config.js文件:（plugins置于module.exports中）
const HtmlWebpackPlugin = require('html-webpack-plugin');
plugins: [
    new CleanWebpackPlugin(['dist']),
    new HtmlWebpackPlugin({
        title: 'Output Management bylhj'
    })
]

运行构建命令npm run build查看效果，将会在dist文件夹中生成新的index.html 文件，替换原来的index.html 文件；

3.清理 /dist 文件夹
首先安装clean-webpack-plugin插件，并且调整 webpack.config.js 文件:
配置webpack.config.js文件:（置于module.exports的plugins中）
const CleanWebpackPlugin = require('clean-webpack-plugin');

new CleanWebpackPlugin(['dist']),

plugins: [
     new CleanWebpackPlugin(['dist']),
     new HtmlWebpackPlugin({
        title: 'Output Management'
     })
]

运行构建命令npm run build查看效果，将会清除原来的dist文件夹内容，加入新的内容；


四、开发
1.使用 source map
为了更容易地追踪错误和警告，JavaScript 提供了 source map 功能，将编译后的代码映射回原始源代码。如果一个错误来自于 b.js，source map 就会明确的告诉你。source map 有很多不同的选项可用，请务必仔细阅读它们，以便可以根据需要进行配置。
我们使用 inline-source-map 选项，这有助于解释说明我们的目的（仅解释说明，不要用于生产环境），配置 webpack.config.js 文件：
（置于module.exports中）
devtool: 'inline-source-map',

写个错误代码，运行构建命令npm run build查看效果，发现浏览器中出现错误的代码文件以及行数；

2.选择一个开发工具
2-1.使用观察模式 watch :
指示 webpack "watch" 依赖图中的所有文件以进行更改。如果其中一个文件被更新，代码将被重新编译，所以你不必手动运行整个构建。
配置 package.json 文件：（在 "scripts" 中加入）
"scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "watch": "webpack --watch",
      "build": "webpack"
    },

在命令行中运行 npm run watch，就会看到 webpack 编译代码，然而却不会退出命令行。这是因为 script 脚本还在观察文件，若webpack 观察文件的同时，我们先移除我们之前引入的错误， webpack 会自动重新编译修改后的模块，唯一的缺点是，为了看到修改后的实际效果，你需要刷新浏览器。如果能够自动刷新浏览器就更好了，可以尝试使用 webpack-dev-server，恰好可以实现我们想要的功能。

2-2.使用 webpack-dev-server
Webpack-dev-server 为你提供了一个简单的 web 服务器，并且能够实时重新加载(live reloading）；
首先安装webpack-dev-server插件，并且调整 webpack.config.js 以及package.json 文件:
npm install --save-dev webpack-dev-server

配置webpack.config.js文件:（置于module.exports中）
devServer: {
    contentBase: './dist'
},

通过配置告知，在 localhost:8080 下建立服务，将 dist 目录下的文件，作为可访问文件，再配置package.json文件，添加一个 script 脚本，可以直接运行开发服务器(dev server):（在 "scripts" 中加入）
"scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "watch": "webpack --watch",
     "start": "webpack-dev-server --open",
      "build": "webpack"
    },

可以在命令行中运行 npm start，就会看到浏览器自动加载页面。如果现在修改和保存任意源文件，web 服务器就会自动重新加载编译后的代码。
【端口号为： localhost:8080 】

2-3.使用 webpack-dev-middlewar
webpack-dev-middleware 是一个容器(wrapper)，它可以把 webpack 处理后的文件传递给一个服务器(server)
首先安装express 和 webpack-dev-middleware插件：
npm install --save-dev express webpack-dev-middleware

先配置webpack.config.js文件:（置于module.exports的 output 中）

output: {
      filename: '[name].bundle.js',
      path: path.resolve(__dirname, 'dist'),
      publicPath: '/'
 }

由于publicPath 也会在服务器脚本用到，以确保文件资源能够在http://localhost:3000下正确访问，我们稍后再设置端口号。下一步就是设置我们自定义的 express 服务，新建一个 server.js 文件于根目录Webpack_Development下面，加入以下内容：（server.js）

const express = require('express');const webpack = require('webpack');const webpackDevMiddleware = require('webpack-dev-middleware');
const app = express();const config = require('./webpack.config.js');const compiler = webpack(config);
// Tell express to use the webpack-dev-middleware and use the webpack.config.js// configuration file as a base.
app.use(webpackDevMiddleware(compiler, {
  publicPath: config.output.publicPath
}));
// Serve the files on port 3000.
app.listen(3000, function () {
  console.log('Example app listening on port 3000!\n');});

再配置package.json文件:（在 "scripts" 中加入）
"scripts": {
      "test": "echo \"Error: no test specified\" && exit 1",
      "watch": "webpack --watch",
      "start": "webpack-dev-server --open",
      "server": "node server.js",
      "build": "webpack"
    },

执行 npm run server，将会重新进行构建项目，打开浏览器，跳转到 http://localhost:3000，你应该看到你的webpack 应用程序已经运行
【注意：webpack-dev-middlewar 要求的node 以及Webpack的环境均为最新环境，目前我的电脑的node 版本为 7.0.0，非最新版本node ，因而无法正常运行，会报错，将node环境提升到最新版本应该就OK了】


五、模块热替换
1.启用 HMR


六、tree shaking
1.


七、生产环境构建
1.

八、代码分离
1.

九、懒加载
1.

十、缓存
1.

十一、创建 library
1.


十二、shimming
1.

十三、渐进式网络应用程序
1.

十四、TypeScript
1.

十五、迁移到新版本
1.

十六、使用环境变量
1.


十七、构建性能
1.

十八、内容安全策略
1.

十九、开发 - Vagrant
1.

二十、管理依赖
1.

二十一、公共路径(public path)
1.


二十二、集成(integrations)
1.





