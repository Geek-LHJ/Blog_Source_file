---
title: "React响应用户输入——coding迪斯尼（慕课网）"
date: 2018-08-06T23:00:06+08:00
draft: true
---

# React响应用户输入——coding迪斯尼（慕课网）

## 第1章 数据逻辑与UI的结合
### 1.1 数据逻辑与UI的结合（1）
1. 建立一个简单的React的例子，效果为一个圆的图片；目的是：将底层的数据逻辑处理过程与前端的UI结合在一起；如何将原有的JavaScript数据结构和React结构结合起来；

### 1.2 数据逻辑与UI的结合（2）
1. 了解JSX的对象的数据格式，我们还可以将JSX对象当做变量来使用，例：var theCircle= <Circle bgColor="#f00"/>;
在React.render()的DOM节点中加入{theCircle}，因而我们可以把数据逻辑设计的很复杂，然后由react框架来解析数据；
在浏览器中显示由Warning，需要给每一个组件加入一个key属性，见下面程序；

```javascript
      var dist= document.getElementById('example');
      class Circle extends React.Component{
        render(){
          var circlStyle={
            padding:10,margin:20,display:"inline-block",
            backgroundColor:this.props.bgColor,borderRadius:"50%",
            width:100, height:100
          };
          return(
            <div style={circlStyle}></div>
          );
        }
      }
      //var theCircle= <Circle bgColor="#f00"/>;
      function showCircle(){
        var colors=["red", "blue", "yellow", "gray","black","pink","#887552","#E94F37"];
        var circleItem= [];
        for(let i= 0; i< colors.length; i++){
          var randNum= Math.floor(Math.random()* colors.length);
          circleItem.push(<Circle bgColor= {colors[randNum]} key={i+ colors[randNum]}/>);
        }
        return circleItem;
      }
      ReactDOM.render(
        <div>
          {showCircle()}
        </div>,
        dist
      );
```

## 第2章 事件处理机制
### 2.1 React的事件处理机制（1）
1. 要实现一个用户交互的简单实例，点击按钮实现数字增加的例子，来解释React的事件处理机制，如何对事件进行监听，还有如何进行事件处理；


### 2.2 React的事件处理机制（2）
1. React如何处理用户的操作事件；
> 一定注意： this的指向问题，若是调用自定义的函数，必须在构造函数constructor中加一条 ，例： this.increase= this.increase.bind(this);    要不然会出现找不到该属性的错误；

2. 在按钮点击事件触发的increase函数中传入的 e 这个参数包含许多知识，通过e可以得知许多与改时间相关的信息，例如鼠标的按键是左键还是右键的信息，或者是键盘当前哪个按钮被按下；实际上 e 指向的是React 所封装的 SyntheticEvent对象，该对象面向的是各种不同的事件所引发的DOM的事件对象；
> SyntheticEvent对象有许多属性，例如bubbles、target、type等等属性，该对象还会封装不同属性，如MouseEvent对象
>>例子：对 shiftKey 的属性测试；见代码【注意setState方法中只能改变state的状态的值】

```javascript
      var dist= document.getElementById('example');
      //子组件显示数字
      class Counter extends React.Component{
        render(){
          var textStyle={
            fontSize:72,color:"#333",fontWeight:"bold"
          };
          return (
            <div style={textStyle}>
              {this.props.display}
            </div>
          );
        }
      }
      //父组件框
      class CounterParent extends React.Component{
        constructor(props){
          super(props);
          this.state= {
            count: 0
          };
          //一定要注意this的执行问题，必须加这句话
          this.increase= this.increase.bind(this);
        }
        //增加count值，注意这个传入的变量 e 里面有许多知识；
        increase(e){
          var curCount= this.state.count;
          if(e.shiftKey == true){
            curCount= curCount + 100
          }else{
            curCount= curCount + 1             
          }            
          this.setState({
            count:curCount
          });
        }
        render(){
          var backgroundStyle= {
            padding:50,backgroundColor:"#ffc53A",width:250,height:100,
            borderRadius:10,textAlign:"center"
          };
          var buttonStyle= {
            fontSize:"1em",width:30,height:30,color:"#333",
            fontWeight:"bold", lineWeight:"3px"
          };
          return(
            <div style= {backgroundStyle}>
              <Counter display= {this.state.count}/>
              <button style= {buttonStyle} onClick= {this.increase}>+</button>
            </div>
          );
        }
      }
      ReactDOM.render(
        <CounterParent/>,
        dist
      );
```

## 第3章 DOM 模型的操作
### 3.1 React 对 DOM 模型的操作 （1）
1. 目的是研究React 框架如何处理最原始的DOM节点元素，通过一个实例来看，在不违背React框架的原则下，通过直接操作DOM元素或使用原生的DOMAPI实现功能，实例效果为输入一个颜色rgb值，在DIV中显示颜色；
> 注意的是在提交后的输入框的内容以及按钮的焦点状态的问题，讨论如何快速解决问题；

### 3.2 React 对 DOM 模型的操作 （2）
1. 实现组件UI框架的构建，以及一些样式的设置；

### 3.3 React 对 DOM 模型的操作 （3）
1. 实现点击按钮，将输入的颜色值展示位颜色的逻辑实现
> 当我们点击按钮时，将input输入框中输入的颜色值设置为当前的state状态中bgcolor的值，render函数重新调用，然后显示颜色的div框中通过调用新状态值进行设置颜色；
>> 小技巧：添加了一个新的标签form，包含提交按钮，设置form的onSubmit函数，调用响应用户点击按钮后的事件函数onSubmit= {this.setNewColor}
### 3.4 React 对 DOM 模型的操作 （4）
1. 解决用户体验差的问题：实现文本内容的自动清空与按钮的焦点自动装换；
> React用的是JSX的语法，JSX实际上是HTML代码格式的延伸；那么如何通过有效的办法去获得原生控件具体的JavaScript对象本身；

> React框架让HTML与JSX控件对象添加了一个桥梁，就是 ref 的属性机制，让我们在JSX里面直接引用到控件本身的JavaScript对象，见代码
>> 多阅读 ref 的相关资料，了解更多用法

```javascript
      var dist= document.getElementById('example');
      class Colorizer extends React.Component{
        //constructor构造器设置初始化的state状态值
        constructor(props){
          super(props);
          this.state={
            color:'',
            bgColor:''
          };
          //一定要绑定组件的函数的this指向
          this.colorValue= this.colorValue.bind(this);
          this.setNewColor= this.setNewColor.bind(this);          
        }
        //获取文本框中输入的内容,注意 e 包含的内容(重要)
        colorValue(e){
          this.setState({
            color:e.target.value
          });
        }
        //用来响应用户点击按钮后的事件,注意 e 包含的内容(重要)
        setNewColor(e){
          this.setState({
            bgColor:this.state.color
          });
          //清除文本框的内容和加入文本框输入焦点
          this._input.value= "";
          this._input.focus();
          console.log(this._input);
          e.preventDefault();
        }
        render(){
          var squareStyle= {backgroundColor:this.state.bgColor};
          var self= this;
          return(
            <div className= "colorArea">
              <div style= {squareStyle} className= "colorSquare"></div>
              <form onSubmit= {this.setNewColor}>
                <input ref= {
                  function(el){
                    self._input= el;
                  }
                } 
                onChange={this.colorValue} placeholder= "Please enter a color:"/>
                <button type="submit">Show</button>
              </form>
            </div>
          );
        }
      }
      ReactDOM.render(
        <Colorizer/>,
        dist
      );
```