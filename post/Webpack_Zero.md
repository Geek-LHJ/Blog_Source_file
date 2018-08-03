---
title: "Webpack_Zero_从零搭建React全家桶框架教程"
date: 2018-07-26T00:00:05+08:00
draft: true
---

# 一、PPT内容：《webpack培训》
1、Webpack本质：JavaScript应用程序的静态模块打包器；
2、Webpack配置的核心组成；


# 二、从零搭建React全家桶框架教程
D:\MyData\Learning\Webpack\react-family        //完成第一个步骤
D:\MyData\Learning\Webpack\Webpack_Demo    //下面全部完成
1、webpack配置步骤：
https://github.com/brickspert/blog/issues/1#issuecomment-326899255

1、安装 webpack
npm install --save-dev webpack@3

2、根据webpack文档编写最基础的配置文件
新建webpack开发配置文件     touch webpack.dev.config.js
加入下面内容：
const path = require('path');
module.exports = {
    /*入口*/
    entry: path.join(__dirname, 'src/index.js'),
    /*输出到dist文件夹，输出文件名字为bundle.js*/
    output: {
        path: path.join(__dirname, './dist'),
        filename: 'bundle.js'
    }
};

3、学会使用webpack编译文件
新建入口文件     mkdir src && touch ./src/index.js
src/index.js 添加内容
document.getElementById('app').innerHTML = "Webpack works"
执行命令 webpack --config webpack.dev.config.js
可以看到生成了dist文件夹和bundle.js

4、现在测试下~
dist文件夹下面新建一个index.html        touch ./dist/index.html
加入下面内容：
<!doctype html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
<div id="app"></div>
<script type="text/javascript" src="./bundle.js" charset="utf-8"></script>
</body>
</html>

浏览器打开index.html,可以看到Webpack works!

2、babel 步骤：
1、安装命令：
npm install --save-dev babel-core babel-loader babel-preset-es2015 babel-preset-react babel-preset-stage-0

2、新建babel配置文件    .babelrc ，
并加入内容：
{
   "presets": [
     "es2015",
     "react",
     "stage-0"
   ],
   "plugins": []
}

3、修改webpack.dev.config.js，增加babel-loader！
/*src文件夹下面的以.js结尾的文件，要使用babel解析*/
/*cacheDirectory是用来缓存编译结果，下次编译加速*/
module: {
     rules: [{
         test: /\.js$/,
         use: ['babel-loader?cacheDirectory=true'],
         include: path.join(__dirname, 'src')
     }]
}

4、测试允许babel转义ES6
修改 src/index.js
/*使用es6的箭头函数*/
var func = str => {
     document.getElementById('app').innerHTML = str;
};
func('我现在在使用Babel!');

然后执行打包命令webpack --config webpack.dev.config.js
浏览器打开index.html，我们看到正确输出了我现在在使用Babel!

3、react 步骤：
1、安装命令：    npm install --save react react-dom
2、修改 src/index.js使用react：
import React from 'react';
import ReactDom from 'react-dom';
ReactDom.render(
    <div>Hello React!</div>, document.getElementById('app'));
3、执行打包命令：    webpack --config webpack.dev.config.js
打开index.html 看效果；
4、把Hello React放到组件里面，体现组件化：
4.1、在src文件夹里面建一个component文件夹，进入component文件夹，再建一个Hello文件夹，进入Hello文件夹，建立一个Hello.js文件；
cd src
mkdir component
cd component
mkdir Hello
cd Hello
touch Hello.js
4.2、按照React语法，写一个Hello组件：
import React, {Component} from 'react';
export default class Hello extends Component {
    render() {
        return (
            <div>
                Hello,React!
            </div>
        )
    }
}

4.3、修改src/index.js，引用Hello组件：
import React from 'react';
import ReactDom from 'react-dom';
import Hello from './component/Hello/Hello';
ReactDom.render(
    <Hello/>, document.getElementById('app'));
4.4、在根目录执行打包命令：    webpack --config webpack.dev.config.js
打开index.html看效果；

5、命令优化
修改package.json里面的script，增加dev-build：
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev-build": "webpack --config webpack.dev.config.js"
  }
直接执行npm run dev-build就可以；

4、react-router步骤：
1、安装命令：    npm install --save react-router-dom
2、新建 router 文件夹和组件：在src 文件夹下面建立router 文件夹，并在router 文件夹里面建立router.js 文件；
cd src
mkdir router && touch router/router.js
3、编写router.js 文件：
import React from 'react';
import {BrowserRouter as Router, Route, Switch, Link} from 'react-router-dom';
import Home from '../pages/Home/Home';
import Page1 from '../pages/Page1/Page1';
const getRouter = () => (
    <Router>
        <div>
            <ul>
                <li><Link to="/">首页</Link></li>
                <li><Link to="/page1">Page1</Link></li>
            </ul>
            <Switch>
                <Route exact path="/" component={Home}/>
                <Route path="/page1" component={Page1}/>
            </Switch>
        </div>
    </Router>
);
export default getRouter;
4、新建页面文件夹 pages，其中建立Home,Page1文件夹，再在Home,Page1文件夹中分别建立Home.js、Page1.js两个页面；
cd src
mkdir pages

cd src/pages
mkdir Home && touch Home/Home.js
mkdir Page1 && touch Page1/Page1.js

Home.js、Page1.js两个页面填充内容：
Home.js内容：
import React, {Component} from 'react';
export default class Home extends Component {
    render() {
        return (
            <div>
                this is home~
            </div>
        )
    }
}
Page1.js内容：
import React, {Component} from 'react';
export default class Page1 extends Component {
    render() {
        return (
            <div>
                this is Page1~
            </div>
        )
    }
}
现在路由和页面建好了，我们在入口文件src/index.js引用Router，修改src/index.js
import React from 'react';
import ReactDom from 'react-dom';
import getRouter from './router/router';
ReactDom.render(
    getRouter(), document.getElementById('app'));
执行打包命令npm run dev-build。打开index.html查看效果；
【注意此时点击‘首页’和‘Page1’没有反应，需要配置一个简单的WEB服务器，下面两种方法来实现：1. Nginx, Apache, IIS等配置启动一个简单的的WEB服务器。2. 使用webpack-dev-server来配置启动WEB服务器】

5、 webpack-dev-server步骤：
webpack-dev-server就是一个小型的静态文件服务器，使用它可以为webpack打包生成的资源文件提供Web服务；
1、安装命令：     npm install webpack-dev-server@2 --save-dev
2、修改webpack.dev.config.js,增加webpack-dev-server的配置：
加入一下内容：
    devServer: {
        contentBase: path.join(__dirname, './dist')
    }
3、执行运行命令
webpack-dev-server --config webpack.dev.config.js
浏览器打开http://localhost:8080，可以点击首页,Page1了
4、优化命令：
修改package.json，增加script->start：
"scripts": {
    "test": "echo \"Error: no test specified\" && exit 1",
    "dev-build": "webpack --config webpack.dev.config.js",
    "start": "webpack-dev-server --config webpack.dev.config.js"
  }
以后直接执行npm start就可以了；
5、webpack-dev-server的其他的配置项：

在webpack.dev.config.js中修改下我们的webpack-dev-server的配置：
devServer: {
    port: 8080,
    contentBase: path.join(__dirname, './dist'),
    historyApiFallback: true,//让所有的404定位到index.html
    host: '0.0.0.0'//指定一个host,默认是localhost。如果你希望服务器外部可以访问,指定如下：host: "0.0.0.0"
}
CLI ONLY的需要在命令行中配置package.json文件：
"start": "webpack-dev-server --config webpack.dev.config.js --color --progress"

6、 模块热替换（Hot Module Replacement）步骤：
w





三、安装 react-app，建立一个react文件：https://github.com/facebook/create-react-app
D:\MyData\Learning\Webpack\react_demo
1、If you use npm 5.1 or earlier, you can't use npx. Instead, install create-react-app globally，then run the command.

npm install -g create-react-app

create-react-app my-app

cd my-app

npm start

【打开http://localhost:3000/】



