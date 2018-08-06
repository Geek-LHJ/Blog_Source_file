---
title: "React组件——coding迪斯尼（慕课网）"
date: 2018-08-06T12:00:06+08:00
draft: true
---

# React组件——coding迪斯尼

## 第1章 初识React
### 1.1 React基本概念

1. 单页模型（SPA）设计难点：
> 如何保持数据和UI同步更新；
如何提高DOM操作效率；
使用HTML开发UI界面异常复杂；

2. React优点：
> 自动化的UI管理：——数据与UI界面之间有一个联合层，开发者只需关心事件;
更高效的DOM操作：——(Virtual DOM)State Change=>Compute Diff=>Re-Render：再到 Browser DOM;
UI的组件化设计：React提供许多API，用于构建小的以及能够重用的组件，再合成大组件；
依赖JS开发UI界面：完全摆脱jss影响，应用jsx的语法结构，JSX实际为自动解读为一系列的DOM操作；
React本质是MVC中的View，特性就是讲数据与UI结合；


### 1.2 React第一个应用

1. 建立一个HTTP服务器：
> 安装Python，cmd中输入 Python -m http.server
例：


```javascript
ReactDOM.render(<h1></h1>, document.querySelector("#test"));
//第一个参数为JSX对象，为需要在界面上显示的元素进行组织；第二个参数是JSX 对应的DOM元素需要挂载的DOM节点；
```

# 第2章 React 组件
## 2.1 react组件化思想

1. React 组件分解：
> 一个复杂的控件拆分为多个小控件的组合，组件化思想与面向对象的程序设计思想基本上一致的，组件可以对应类，设计接口就行，提高组件代码的重用性；

2. 组件与函数
> 组件把绘制界面的逻辑包装起来，通过给组件传入不同的参数来改变组件的呈现效果，复杂的组件还可以转化为多个小组件的组合；


## 2.2 helloworld 组件
> 通过React.createClass定义组件类，例：

```javascript
var Hello= React.creatClass({
    render: function(){
        return (<div>test,{this.props.name}</div>);//this.props方法调用实例中的属性
    }
});
//实例组件，调用接口多次复用
ReactDOM.render(
    <div>
        <Hello name= "jack"/>
        <Hello name= "tonny"/>
        <Hello name= "Nancy"/>
    </div>
    ,document.querySelector("#container")
)
```

> 通过React.createClass对组件进行定义，可以实现对于组件的复用；

## 2.3 React 组件的样式设计（1）
> 继续练习对于组件的创建，通过一个简单的例子理解创建过程;
>> 见2.4中代码

## 2.4 React 组件的样式设计（2）
1. 设计思维逻辑
> React组件化设计的原则是要把控件的界面设计逻辑和控件所要实现的业务逻辑放在同一个地方；React的做法是，把界面的设计逻辑封装成一个JSON对象，把这个JSON对象就放在这个React代码模块中；

```javascript
//通过React.createClass 创建一个名为Letter的组件对象，this.props.children方法调用其子元素
      var  Letter= React.createClass({        
        render: function(){
        //React设计原则：界面设计逻辑和控件所要实现的业务逻辑放在同一个地方
        var letter= {
          padding: 10,
          margin: 10,
          backgroundColor: this.props.bg,
          color: "#333",
          display: "inline-block",
          fontSize: 32,
          textAlign: "center"
        };
          return (
            /*<div className= "letterStyle">{this.props.children}</div>*/
            <div style={letter}>{this.props.children}</div>

          );
        }
      });
      var dist= document.querySelector("#container");

      ReactDOM.render(
        <div>
          <Letter bg="red">A</Letter>
          <Letter bg="green">B</Letter>
          <Letter bg="blue">C</Letter>
          <Letter bg="yellow">D</Letter>
          <Letter bg="gray">E</Letter>
          <Letter bg="#cc0">F</Letter>
        </div>,dist
        );
```

## 2.5 设计复合式控件（1）
1. 设计一个显色板，包括上面的显色板组件和下面的白色文本框，由一个大控件包含两个组件；
> 代码见 2.7 中

## 2.6 设计复合式控件（2）
1. 通过this.props方式进行父子组件之间的值传递；父组件为Card，子组件分别是显色板控件Square，文字显色控件Square；
> 代码见 2.7 中

## 2.7 实现复合式控件
1. 实现了通过改变父组件Card的color属性，来分别在子组件Square、Square进行获取并使用；

```javascript
//显色板控件,颜色获取方式为this.props.color，指向Card父组件
      var Square= React.createClass({
        render: function(){
          var squareStyle= {
            height: 150,
            backgroundColor: this.props.color
          };
          return (
            <div style= {squareStyle}>
            </div>
          );
        }
      });
    //文字显色控件,颜色获取方式为this.props.color，指向Card父组件
      var Label= React.createClass({
        render:function(){
          var labelStyle= {
            fonFamily: "sans-serif",
            fontWerght:"bold",
            padding: 13,
            margin: 0
          };
          return (
            <div style= {labelStyle}>
              <p>{this.props.color}</p>
            </div>
          );
        }
      });
    //父控件，,颜色获取方式为this.props.color，，指向Card组件实例化时，设置其color属性，用于构建该组件时调用对象
      var Card= React.createClass({
        render: function(){
          //设置父控件的样式
          var cardStyle= {
            height: 200,
            width:150,
            backgroundColor: "#fff",
            WebkitFilter: "drop-shadow(0px 0px 5px #666)",
            filter: "drop-shadow(0px 0px 5px #666)"
          }
          return(
            <div style= {cardStyle}>
              <Square color={this.props.color}/>
              <Label color={this.props.color}/>
            </div>
          );
        }
      });
      //Card组件实例化时，设置其color属性，用于构建该组件时调用
      ReactDOM.render(
        <Card color= "blue"/>,
        document.getElementById('example')
      );
```

## 2.8 组件的属性传递机制（1）
1. React的属性传递的特性：
> 组件之间的传递是通过上一层向下一层传递的，不能跨层传递属性；同时，子组件不能向父组件传递属性值；

2. 该机制的问题：
> 传递多个属性值很麻烦；该方法很难扩展和维护；

## 2.9 组件的属性传递机制（2）
1. 构建三个组件，尝试传递数据，从外层到里层，组件分别为：Shirt=> Label=> Display;当属性很多时，利用ES6 的属性扩展操作符（...)来替换，代码如下：
```javascript
//最里层组件Display
      var Display= React.createClass({
        render: function(){
          return (
            <div>
              <p>{this.props.color}</p>
              <p>{this.props.num}</p>
              <p>{this.props.size}</p>
            </div>
          );
        }
      });

      //第二层组件Label
      var Label= React.createClass({
        render: function(){
          return (
            /*<Display color={this.props.color} num={this.props.num} size= {this.props.size}/>          */
            <Display {...this.props} />
          );
        }
      });

      //最外层组件Shirt
      var Shirt= React.createClass({
        render: function(){
          return (
            /*<Label color={this.props.color} num={this.props.num} size= {this.props.size}/>          */
            <Label {...this.props} />
          );
        }
      });

      //渲染到真正DOM节点
      ReactDOM.render(
        <Shirt color="blue" num="2" size="middle"/>,
        document.getElementById('example')
      );
```

## 2.10 组件的状态机制（1）
1. 由于组件的属性在浏览器加载后将不再变化，但是由于程序的需求实在一个活的情境中，需要一个灵活的机制，让组件能够应用于变化的场景中，因而需要一种除了属性之外的存储机制，适用于场景的变化，并且对变化有应对的机制，这个便是组件的状态；通过实践来认识组件的状态；

## 2.11 组件的状态机制（2）
1. 设计实现一个变化数据的组件，父组件LightCounterDisplay，子组件LightCounter；

## 2.12 组件的状态机制（3）
1. 子组件LightCounter改进为在里面设计一个自增的变量，并显示出来；

>> 由于React在ES6的实现中去掉了getInitialState这个hook函数，规定state在constructor中实现；

## 2.13 组件的状态机制（4）
1. 程序代码：
```javascript
//子组件LightCounter，用于显示字符串；改进为在里面设计一个自增的变量，并显示出来
      /*var LightCounter= React.createClass({*/
      //React在ES6的实现中去掉了getInitialState这个hook函数，规定state在constructor中实现
      class LightCounter extends React.Component{
        
        constructor(props){
          super(props);
          this.state={ strikes: 0, };
        }

        timertick(){
          //setState用于修改组件本身的state对象,传入的为JSON数据，覆盖之前的state对象值
          this.setState({
            strikes: this.state.strikes +100
          });
        }
        //初识化数据时调用的借口方法,ES6 已经废弃该方法
        /*getInitialState:function(){
          return{
            strikes: 0
          };
        },*/

        //组件在被浏览器加载后，但是render函数还没有被调用前
        componentDidMount(){        
        //通过setInterval方法产生定时器，进行变量变化
          setInterval(this.timertick, 1000);
        }
      
        //渲染真实的DOM节点
        render(){ 
          var counterStyle= { color: "#66ffff", fontSize: 50 };
          var count= this.state.strikes.toLocaleString();
          return(
            <h1 style={counterStyle}>{count}</h1>
          );
        }
      }

      //父组件LightCounterDisplay，用于绘制黑色的块
      var LightCounterDisplay= React.createClass({
        render: function(){
          var divStyle= { width: 250, backgroundColor: "black", textAlign: "center",padding: 40,color: "#999",borderRadius: 10};
          var comonStyle= { margin: 0, padding: 0 };
          //...操作符的使用，来融合不同的样式
          var textStyle= {
            emphasis:{ fontSize:38, ...comonStyle },
            smallEmphasis:{ ...comonStyle },
            small:{fontSize:17, opacity: 0.6, ...comonStyle }
          };
          return(
            <div style={divStyle}>
              <LightCounter />
              <h2 style= {textStyle}> 雷霆打击</h2>
              <p style= {textStyle.emphasis}> 我们的地球</p>
              <p style= {textStyle.smallEmphasis}> (自从添加组件开始)</p>

            </div>
          );
        }
      });
      
      //组件渲染
      ReactDOM.render(
        <LightCounterDisplay />,
        document.getElementById('example')
      );
```

# 第3章 React生命周期
## 3.1 React 组件的生命周期（1）
1. 生命周期函数就是组件本身具备的一些固定接口，这些接口被框架在适当的时间去调用，大致有以下几种：（代码3-6）

> componentWillMount：组件最初状态渲染
>> render 函数实现state 更新
>>> componentDidMount： 组件最初状态渲染完成

> shouldComponentUpdate：组件是否根据新的变化更新
>> componentWillUpdate： 组件将要更新
>>> render 函数实现state 更新
>>>> componnetDidUpdate： 组件完成更新

> componentWillUnmount： 组件销毁

> componentWillReceiveProps： 组件的属性将变化

## 3.2 React 组件的生命周期（2）
1. 通过一个实例说明组件的各个生命周期函数；（代码3-6）

## 3.3 React 组件的生命周期（3）
1. getDefaultProps()和getInitialState()在ES6中均废弃，在通过Class创建新的组件对象时，其中的静态属性 static 设置可以替代getDefaultProps()接口，constructor 构造器可以替代和getInitialState()接口；（查看代码注意写法）（代码3-6）
## 注意：this的指向问题，需要在 constructor 中加入对于调用函数的this指向为该新建的组件对象，而不是全局window对象；或者是通过构造函数来解决该问题；

## 3.4 React 组件的生命周期（4）
1. shouldComponentUpdate 方法是在用户有操作改变state状态后，将第一个调用的函数，有两参数：(newProps,newState),返回true则进行更新，返回false将终止更新，生命周期停止；（代码3-6）


## 3.5 React 组件的生命周期机制（上）
1. componentWillUnmount 方法用于组件销毁前，通知做一些收尾工作，例如释放内存，定时器等；通过React的ReactDOM.unmountComponentAtNode() API 接口调用，传入的参数为组件插入的具体DOM节点，如:document.getElementById('example');（代码3-6）

## 3.6 React 组件的生命周期机制（下）

1. componentWillReceiveProps： 组件的属性将变化；
Props的变化和state的变化是一致的，

```javascript
//子组件Counter
      class Counter extends React.Component{
        //组件将接收新的props属性值
        componentWillReceiveProps(newProps){
          console.log("componentWillReceiveProps: component  Receive new Props");
          return ;
        }
        //判断是否更新新的属性
        shouldComponentUpdate(newProps, newState){
          console.log("shouldComponentUpdate： should counter Update？");
          return true;
        }
        //组件将要更新，然后触发render函数进行更新组件
        componentWillUpdate(){
          console.log("componentWillUpdate:  counter will  Update.");
          return;
        }
        //组件完成更新
        componentDidUpdate(){
          console.log("componentDidUpdate:  counter did Update.");
          return;
        }
        //组件进行渲染
        render(){
          var textStyle= {fontSize: 72,color:"#333", fontWeight:"bold"}
          return (
            <div style= {textStyle}>{this.props.display}</div>
          );
        }
      }

      //父组件CounterParent
      class CounterParent extends React.Component{
        /*getDefaultProps:function(){
          console.log("getDefaultProps:receive props from outsize");
          return {};//返回的为this.props 的JSON对象
        }*/

        //Use a static property to define defaultProps instead,instead getDefaultProps() 
        static DefProps() {
          console.log("getDefaultProps:receive props from outsize");
          this.props= {};
        }

        /*getInitialState:function(){
          console.log("getInitialState:set default state object");
          return {};//返回this.state 的初始值
        },*/
        //构造器函数取代了getInitialState()方法
        constructor(props){
          console.log("getInitialState:set default state object");
          super(props);
          this.state = { count: 0 };
          this.increase= this.increase.bind(this);
        }
        //组件将要初始化渲染，然后触发render函数进行渲染组件
        componentWillMount(){
          console.log("componentWillMount: component Will about to mount");        
          return;
        }
        //组件完成初始化渲染
        componentDidMount(){
          console.log("componentDidMount: component is just mount");
          return;
        }
        //state状态的count 数自增
        increase(){
          this.setState({
            count: this.state.count+ 1
          });
        }
        //组件接收新的state值后是否要进行更新操作
        shouldComponentUpdate(newProps, newState){
          console.log("shouldComponentUpdate： should Component Update ？");
          if(newState.count < 5){
             console.log(" Component should Update!");
             return true;
          }else{
            console.log(" Component should not Update!");
            ReactDOM.unmountComponentAtNode(document.getElementById('example'));
            return false;
          }          
        }
        //组件即将销毁时调用，通过React的API接口 ReactDOM.unmountComponentAtNode() 触发
        componentWillUnmount(){
          console.log("componentWillUnmount:  Component is about to removed from dom.");

        }
        //组件将要更新，然后触发render函数进行更新组件
        componentWillUpdate(){
          console.log("componentWillUpdate:  Component is about to Update.");
          return;
        }
        //组件完成更新
        componentDidUpdate(){
          console.log("componentDidUpdate:  Component is just Update.");
          return;
        }
        //组件渲染
        render(){
          var backgroundStyle= { padding: 50, border:"1px dotted #333",
            width: 250, height: 100, borderRadius:10, textAlign:"center"
          }
          //var s= "CounterParent rendering ...";
          return(
            <div style= {backgroundStyle}>
              <Counter display= {this.state.count}/>
              <button onClick= {this.increase}>+</button>
            </div>
          );
        }
      }

      ReactDOM.render(
        <CounterParent />,
        document.getElementById('example')
      );
```