---
title: "React.js 小书笔记"
date: 2018-08-07T23:00:06+08:00
draft: true
---


# React.js 小书笔记
>> [git下载地址：](https://github.com/Geek-LHJ/Coding_Practice)
## 第一阶段 
### 1.1 react简介
1. 

### 1.2 前端组件化（1）
1. 

### 1.3 前端组件化（2）
1. 

### 1.4 前端组件化（3）
1. 


### 1.5 React.js 基本环境安装
1. 

### 1.6 使用 JSX 描述UI信息
1. 简单的例子：

> 注意观察各个部分的书写格式；

```javascript
import React ,{Component} from  'react'
import ReactDOM from 'react-dom'
import './Myindex.css'
//创建Header组件对象
class Header extends Component{
    render(){
        return(
            <div>
                <h1 className= "title">React小书</h1>
            </div>
        );
    }
}
//将JavaScript对象渲染到真实的DOM节点上
ReactDOM.render(
    <Header />,
    document.getElementById('root')
)
```

2. JSX 原理，讨论其底层是如何实现的；【JSX 是JavaScript语言的扩展，实际上就是 JavaScript 对象】

> 用JavaScript对象来表现一个DOM元素结构，每个DOM元素包含的信息有三个：标签名，属性，子元素；

### 1.7 组件 render 方法
1. React.js 中一切皆组件，每一个组件类必须实现一个 render 方法，该方法必须返回一个 JSX 的元素；

> 注意：只能返回一个外层的标签，返回多个报错；

2. 表达式插入:JSX中可以插入 JavaScript表达式，表达式必须以 {} 来包裹；

> {} 中可以放任何的 JavaScript的代码，包括变量、表达式计算、函数执行等， render 会将这些代码返回的内容渲染到页面上；

3. JSX 中的样式类使用的是 className ,不是 class；

4. 条件返回：在 {} 中进行三元操作符的使用，返回结果；
 
### 1.8 组件的组合、嵌套和组件树
1. 组件的复用性很强，我们可以在组建中调用其他的组件；

> 注意：自定义的额组件必须以大写字母开头；

```javascript
//Page组件中调用之前创建的三个小组件
class Page extends Component{
    render(){
        return(
            <div>
                <Header/>
                <Body/>
                <Footer/>
            </div>
        );
    }
}
```

### 1.9 事件监听
1. 监听用户的动作，我们只需要给需要监听的事件元素加上属性类似于 onClick、 onKeyDown 这样的属性即可；

2. React.js 封装了不同类型的事件，可以参考学习 [SytheticEvent - react](https://reactjs.org/docs/events.html#supported-events)

> 没有经过特殊处理的话，这些 on*  的事件监听只能用在普通的的HTML 的标签上，不能用在组件的标签上；

3. event 对象：事件监听函数会被自动传入一个 <b>event</b> 对象，该对象与普通浏览器的event 对象所包含的方法和属性均一致，区别是React的 event 对象是内部构建的，并非浏览器所提供；因而，React.js 中，该对象对外提供统一的API 和 属性，而不需要考虑浏览器兼容的问题；

```javascript
handleClickOnBody(e){
        alert('click on body!');
        //通过 event 对象的e.target.innerHTML对应标签中的内容，并打印
        console.log(e.target.innerHTML);
    }
```

4. this 的指向：一般在某个类的实例方法里面的 this 的指向是实例本身，但是在类中的函数里面的this时，会输出为 null 或者 undefined；这是因为React.js 调用方法的时候，不是通过对象的方式调用的函数，而是直接通过函数调用，所以事件监听函数内并不能通过 this 获取到实例；若要在事件函数中使用当前的实例，需要手动将实例方法 bind 到当前的实例上再传入React.js ;或者用ES6 最新语法箭头函数也可以解决该问题；

```javascript
render(){
        return(
            <div onClick= {this.handleClickOnBody.bind(this)}>
                <h2>React body 部分</h2>
            </div>
        );
    }

//箭头函数写法，解决this的指向,或者是调用时加入bind(this)
    handleClickOnBody=(e)=>{...}
```

### 1.10 组件的state 和setState
1. React中的state是用于存储组件的状态；

> 一个组件的显示形态可以由它的数据状态和配置参数决定；

2. setState方法： 接收对象或者是函数作为参数

> setState 方法由父类 Component 提供，当我们调用这个函数时，React.js 会更新组件的状态 state ，并且重新调用 render 函数，将最新的状态渲染到页面上去；例：

```javascript
class Likebutton extends Component{
    //构造器中初始化state状态
    constructor(){
        super();
        this.state={ 
            isLiked:false,
            count:0 
        }
    }
    //点击按钮触发状态改变
    handleClickOnLikeButton(){
        //接收对象作为参数
        this.setState({
            isLiked: !this.state.isLiked
        })
        //接收函数作为参数
        const preveState= this.state;
        this.setState((preveState)=>{
            return{count: preveState.count +10};//count 数值加 10
        })
    }
    //渲染页面
    render(){
        return(
            <div>
                <p>是否点赞？</p>
                <button onClick= {this.handleClickOnLikeButton.bind(this)}>
                    {this.state.isLiked? '取消' : '点赞'}
                </button>
                <p>count:{this.state.count}</p>
            </div>
        );
    }
}
```


### 1.11 配置组件的 props
1. render 函数中可以看出，组件内部是通过 this.props 的方式获取到组建的参数的，若 this.props 里面有需要的属性就采用，没有则采用默认属性；

```javascript
//创建Likebutton2组件对象
class Likebutton2 extends Component{
    //通过static静态变量设置默认的props,取代后面的 || 的设置
    static defaultProps= {
        liketest: '取消',
        unliketest: '点赞'
    }
    //构造器中初始化state状态
    constructor(){
        super();
        this.state={ isLiked:false,count:0 }
    }
    //点击按钮触发状态改变
    handleClickOnLikeButton(){
        //接收对象作为参数
        this.setState({
            isLiked: !this.state.isLiked
        })        
    }
    //渲染页面
    render(){    
        const liketest= this.props.liketest || '取消';
        const unliketest= this.props.unliketest || '点赞';
        return(
            <div>
                <p>Likebutton2</p>
                <button onClick= {this.handleClickOnLikeButton.bind(this)}>
                    {this.state.isLiked? liketest : unliketest}
                </button>
            </div>
        );
    }
========================================================
    //在另一个大的组组件中设置 Likebutton2 的props属性
    render(){
        return(
            <div>
                <Header/>
                <Body/>
                <Footer/>
                <Likebutton/>
                <Likebutton2 liketest= '已赞' unliketest= '赞'/>
            </div>
        );
    }
```

2. 设置默认的 defaultProps，代码建上方示例代码中；

3. props 不可变原则：React.js 希望一个组件在输入在输入确定的 props 时，能够输出确定的UI显示状态，因而渲染过程中props不可修改；组件使用者可以主动的通过重新渲染的方式把新的props 传入组件中，组件的显示形态将得到变化；

### 1.12 state VS props
1. state ：让组件控制自己的状态

> 主要作用是用于组件保存、控制、修改自己的可变状态；state在组建的内部初始化，可以被组件自身修改，而外部不能访问也不能修改；可以认为state是一个局部的、是能被组件自身控制的数据源；state状态通过this.setState 方法进行更新，setState会导致组件重新渲染；

2. props ：让外部队组建进行配置

> 主要作用是让使用该组件的父组件可以通过传入桉树来配置该组件；它是外部传进来的配置参数，组件内部五大控制修改；只有当外部主动传入新的 props 后，组件的props 才会改变；

3. 无状态组件：不加人状态以及props属性

4. 函数式组件与继承 Component 来构建组件的区别：
函数式组件只接受props，不接受在constructor里面初始化state，函数式组件就是只能接受props 和提供render方法的类组件；

> 函数式组件示例代码：

```javascript
//函数式组件的创建
const HelloWorld= (props)=>{
    const sayHi= (event)=> alert('Hello world!');
    return(
        <div onClick= {sayHi}>helloworld 点我看看</div>
    );
}
```

### 1.13 渲染列表数据
1. 若把数组放入 {} 中，React.js 会把 {} 数组里面的每个元素罗列并渲染出来；

2. 使用 map 渲染列表数据

```javascript
//数据源users
const users = [
    { username: 'Jerry', age: 21, gender: 'male' },
    { username: 'Tomy', age: 22, gender: 'male' },
    { username: 'Lily', age: 19, gender: 'female' },
    { username: 'Lucy', age: 20, gender: 'female' }
];
//使用map函数遍历数据源Datalist
class Datalist2 extends Component{
    render(){
        return(
        <div>
            {users.map((user)=>{
                return(
                <div key={user.username}>
                    <div> 姓名：{user.username}</div>
                    <div> 年龄：{user.age}</div>
                    <div> 性别：{user.gender}</div>
                    <hr/>
                </div> 
                )
            })}
        </div>);
    }
}
```

### 1.14 实战分析：评论功能（1）

1. 组件划分：React.js 中一切接组件，当我们拿到了一个需求后，首先应该理解需求、分析需求、划分这个需求由哪些组件构成；

> 划分组件的目的是为了代码的可复用性和可维护性；

2. 该评论功能的组件划分：整个大组件为 CommentApp ，包含 CommentInput 组件和 CommentList 组件，其中CommentList 组件中包含多个单个的  Comment 评论条小组件；

3. 组件的实现:

> 先利用 create-react-app 构建一个新的工程：    【cmd中】 create-react-app react-comment-app

> 再在 src 目录下建立上述的四个文件：CommentApp.js、CommentInput.js、CommentList.js和Comment.js，再实现一个最基本的组件嵌套的功能,对整个大组价加入一定的样式显示；

### 1.15 实战分析：评论功能（2）

1. 处理用户输入：CommentInput.js 文件

> 加入HTML 的框架，包括用户名、用户名的输入框、评论内容、输入的内容区和提交的按钮；

2. 数据处理逻辑：

> 加入构造器函数 constructor ，里面填写state状态初始化数据，包含用户名输入框和评论内容，分别设置为空字符；this.state= {username:'', content:''}

```javascript

```


3. 用户输入框、内容区分别设置其 value 属性为{this.state.username}、{this.state.content}，以备后面的大组价CommentApp通过props属性获取CommentInput组件中输入的用户名以及内容数据，实现父组件CommentApp获取到子组件CommentInput的数据，如下代码所示：
>> 【注意此处书写的代码的巧妙之处，不同于之前利用props属性将数据从父组件传递到子组件，此处为逆向传递数据】

```javascript
/* 父组件CommentApp中 */
//构造器初始化state状态，设置初始保存的内容数组为空
    constructor(){
        super();
        this.state= {
            comments:[]
        }
    }
    //handleSubmitContent函数获取子组件CommentInput的输入内容
    handleSubmitContent(comment){
        // console.log(comment);
        if(!comment) return
        if(!comment.username) return alert('请输入用户名')
        if(!comment.content) return alert('请输入评论内容')
        this.state.comments.push(comment);
        this.setState({
            comments:this.state.comments
        });
    }
    //渲染到页面
    render(){
        return(
            <div className= "wrapper">
                {/* <p>hello React</p> */}
                <CommentInput onSubmit= {this.handleSubmitContent.bind(this)}/>
                <CommentList comments= {this.state.comments}/>
            </div>
        );
    }
==============================================
/* 子组件CommentInput中 */
//handleSubmit函数点击发布按钮触发内容提交
    handleSubmit(){
        if (this.props.onSubmit){
            const {username, content}= this.state;
            this.props.onSubmit({username, content});
        }
        this.setState({
            content: ''
        });
    }
```

### 1.16 实战分析：评论功能（3）
1. 数据显示组件 CommentList.js

> 先尝试模拟一组用户加内容的数组数据，先实现这个组件对数据的显示功能；通过 map 函数实现对于数组数据中的对象取值（render 函数中），如下代码所示：

```javascript
    return(
        <div >
            {this.props.comments.map((comment, i)=> <Comment comment= {comment} key= {i}/> )}
        </div>
    );
```

2. 单个显示的组件 Comment.js

> 先设计这个组件返回的HTML的框架，设置相应的样式；

> 数据信息则是通过 props 属性获取父组件中的内容数据对象，分别将用户名和内容信息解析到不同的地方，如下代码所示：

```javascript
{this.props.comment.username}

{this.props.comment.content}
```

3. 在去掉模拟数据源，通过获取用户的提交数据作为数据源

> 数据显示组件 CommentList 是通过props 属性从父组件 CommentApp 中获取的数据，如下代码所示：

```javascript
{this.props.comments.map((comment, i)=> <Comment comment= {comment} key= {i}/> )}
```

4. 测试显示map 报错，是由于map遍历的comments数组为用户输入数据，当用户还没有输入数据时，为空，则会报错；防止这个错误产生，我们可以通过static静态方法设置默认的props属性，设置其内的comments为一个空数组对象；
```javascript
static defaultProps={
        comments:[]
    }
```

#### 【演示效果能够达到基本要求】

## 第二阶段 
### 2.17 前端应用状态管理——状态提升 
1. 


### 2.18 挂载阶段的组件生命周期（1）
1.

### 2.19 挂载阶段的组件生命周期（2）
1.

### 2.20 更新阶段的组件生命周期
1.

### 2.21 ref 和 React.js中的DOM操作
1.

### 2.22 props.children 和容器类组件
1.

### 2.23 dangerouslySetHTML 和 style 属性
1.

### 2.24 PropTypes 和组件参数验证
1.

### 2.25 实战分析：评论功能（4）
1.

### 2.26 实战分析：评论功能（5） 
1.

### 2.27 实战分析：评论功能（6）
1.

```javascript

```

## 第三阶段 
### 3.28 高级组件
1.

### 3.29 React.js 的context
1.

### 3.30 动手实现 Redux（1） 
1.

### 3.31 动手实现 Redux（2）
1.


### 3.32 动手实现 Redux（3）
1.


### 3.33 动手实现 Redux（4）
1.


### 3.34 动手实现 Redux（5）
1.


### 3.35 动手实现 Redux（6）
1.


### 3.36 动手实现 React-redux（1）
1.

### 3.37 动手实现 React-redux（2）
1.

### 3.38 动手实现 React-redux（3）
1.

### 3.39 动手实现 React-redux（4）
1.

### 3.40 动手实现 React-redux（5）
1.

### 3.41 动手实现 React-redux（6）
1.

### 3.42 使用真正的Redux 和 React-redux
1.

### 3.43 smart 组件 VS Dumb 组件
1.

### 3.44 实战分析：评论功能（7）
1.

### 3.45 实战分析：评论功能（8）
1.

### 3.46 实战分析：评论功能（9）
1.


```javascript

```
