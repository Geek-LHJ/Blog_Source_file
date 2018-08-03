---
title: "JavaScript学习笔记_W3cschool"
date: 2018-07-26T00:00:02+08:00
draft: true
---

# JavaScript知识点（已学习到）
JavaScript 教程
```javascript
1、JavaScript简介
（1）直接写入HTML输出流：例：document.write("<p>这是一个段落</p>");
        【注：只能在HTML输出中使用，若在文档加载完毕后使用该方法，会覆盖整个文档】
（2）对事件的反应：例：onclick事件；
（3）改变HTML内容：例：document.getElementById("").innerHTML="Hello World";
（4）改变HTML样式：例：document.getElementById("").style.color="#000";
（5）验证输入：例：if语句；

2、JavaScript知识图谱——重要
（1）Javascript数组
（2）JavaScriptDOM基本操作
（3)  JavaScript变量
（4）JavaScript函数基础
（5）JavaScript运算符
（6）JavaScript流程语句
（7）JavaScript数据类型
（8）JavaScript正则表达式
（9）JavaScript字符串函数
（10）Window对象

3、JavaScript用法
（1）<script></script>标签中使用，可以在<head>和<body>中使用，也可以用外部文件：例：
 <script src="xxx.js"></script>
【外部CSS样式引入为：<link type="text/css" rel="stylesheet" href="xxx.css"/>】

4、JavaScript输出
（1）window.alert()弹出警告框
（2）document.write()将内容写到HTML文档中
（3）innerHTML写入到HTML元素
（4）console.log()写入到浏览器控制台

5、JavaScript语法
（1）字面量：数字字面量Number（整数、小数、科学计数e）、字符串字面量String（使用单引号双引号）、表达式字面量（用于计算）、数组字面量Array（定义数组，中括号包含）、对象字面量Object（定义对象，大括号包含）；
（2）JavaScript变量：var关键字定义
（3）JavaScript操作符
（4）JavaScript语句：分号隔开
（5）JavaScript关键词
（6）JavaScript标识符：必须以字母、下划线或美元符开始，后续字符可以是字母、数字、下划线或美元符
（7）JavaScript注释：双斜杠//
（8）JavaScript函数：
（9）JavaScript数据类型五种基本数据类型（Number、String、Boolean、Null、Undefined）一种复杂数据类型(Object)
（10）JavaScript对大小写敏感
（11）JavaScript字符集

6、JavaScript语句
（1）JavaScript语句：分号隔开
（2）JavaScript代码块：大括号括起来
（3）JavaScript语句标识符（关键字）：break、catch、continue、do-while、for、for-in、function、if-else、return、switch、throw、try、var、while等

7、JavaScript注释
（1）单行注释：//
（2）多行注释：/*xxxxxxxxx*/

8、JavaScript变量（学习脑图）
（1）声明（创建）变量：var关键字，此时变量值为undefined；
（2）变量赋值：=

9、JavaScript数据类型（学习脑图）
（1）JavaScript六大数据类型：分别为五种基本数据类型（Number、String、Boolean、Null、Undefined）和一种复杂数据类型(Object)；
（2）JavaScript拥有动态数据类型，相同的变量可用作不同的类型；

10、JavaScript函数（学习脑图）
（1）JavaScript中，函数即对象，可随意被程序操控，函数可以嵌套在其他函数中定义；
（2）JavaScript局部变量：函数内部声明的变量（局部变量比同名的全局变量优先级高，因而会隐藏同名的全局变量）
（3）JavaScript全局变量：函数外声明，网页上所有脚本和函数都能访问它
（4）JavaScript变量生存期：其生命期从他们被声明的时间开始，局部变量在函数运行后删除，全局变量在页面关闭后删除。
（5）向未声明的JavaScript变量分配值：该变量会自动作为全局变量

11、JavaScript作用域（作用域指的是可以访问的变量的集合）
（1）类似于局部变量、全局变量、以及变量生存期的概念

12、JavaScript事件（指的是可以被JavaScript侦测的行为）
（1）html事件：可以是浏览器行为，也可以是用户行为，例：HTML页面加载完成、HTML按钮被点击；
<some-HTML-element some-event="some JavaScript">
（2）常见HTML事件：onchange、onclick、onmouseover、onmouseout、onkeydown、onlooad等；

13、JavaScript字符串（用于存储和处理文本）
（1）JavaScript字符串可使用单引号或者双引号，通过索引来访问字符串每个字符，索引从0开始。
（2）字符串长度使用内置属性length来计算，例：var alen= xxx.length;
（3）字符串可以是对象：new关键字（尽量少用String对象，它会拖慢执行进度）
（4）字符串的属性和方法：
属性及描述：
constructor：返回创建字符串属性的函数；
length：返回字符串的长度；
prototype：允许您向对象添加属性和方法；
方法及描述：
charAt()：返回指定索引位置的字符
charCodeAt()：返回指定索引位置字符的Unicode值
concat()：连接两个或多个字符串，返回连接后的字符串
fromCharCode()：将字符转换为Unicode值
indexOf()：返回字符串中检索指定字符第一次出现的位置
lastIndexOf()：返回字符串中检索指定字符最后一次出现的位置
localeCompare()：用本地特定的顺序来比较两个字符串
match()：找到一个或者多个正则表达式的匹配
replace()：替换与正则表达式相匹配的子串
search()：检索与正则表达式相匹配的值
slice()：提取字符串的片段，并在新的字符串返回被提取的部分
split()：将字符串分割为子字符串数组
substr()：从起始索引号提取字符串中指定数目的字符
substring()：提取字符串中两个指定的索引号之间的字符
toLocalLowerCase()：根据主机的语言把字符串转化为小写
toLocalUpperCase()：根据主机的语言把字符串转化为大写
toLowerCase()：把字符串转化为小写
toUpperCase()：把字符串转化为大写
toString()：返回字符串对象值
trim()：移除字符串首尾空白
valueOf()：返回某个字符串对象的原始值

14、JavaScript运算符（学习脑图）
（1）JavaScript算术运算符：+, -, *, /, %, ++, --
（2）JavaScript逻辑运算符：=, +=, -=, *=, /=, %=
（3）JavaScript字符串连接运算符：加号（+）

15、JavaScript比较和逻辑运算符（用于测试true或者false）
（1）JavaScript比较运算符：==, ===, =, >, <, >=, <=
（2）JavaScript逻辑运算符：&&,||,!
（3）javaScript条件运算符：例： var age= 15; voteable= (age< 18)?"年龄太小":"年龄已达到"；

16、JavaScript流程语句（学习脑图）
（1）循环语句：while、do-while、for、for-in
（2）跳转语句：return、continue、break
（3）选择语句：if-else、switch-case
（4）异常处理语句：throw、try-catch、finally

17、JavaScript if-else语句
（1）条件语句：if、if...else、if...elseif...else、switch、三目运算

18、JavaScript switch语句
（1）语法：
switch(n){
case 1: 代码块1; break;
case 2: 代码块2; break;
case 3: 代码块3; break;
default:代码块;}
//default用于匹配规则不存在时做的事情

19、JavaScript for循环
（1）for(语句1-初始化; 语句2-循环条件; 语句3-循环后执行自增或自减){代码块}
（2）for-in循环：遍历对象的属性或者遍历数组，例：
var x; var txt= "";
var person={name:"jack", age:25};
for(x in person){txt= txt +person[x];}

20、JavaScript while循环
语法：while(条件){代码块}
do{代码块}while(条件)

21、JavaScript Break和Continue语句
（1）break语句跳出循环
（2）continue语句跳出循环中的一个迭代

22、JavaScript类型转换
（1）Number()转化为数字、String()转化为字符串、Boolean()转化为布尔值。
（2）JavaScript数据类型：
五种不同数据类型：string、number、boolean、object、function
三种对象类型：Object、Date、Array
两种不包含任何值的数据类型：null、undefined
（3）typeof 操作符：查看变量的数据类型【null 返回为object类型；NaN是number类型；Array是object类型；date是object类型；未定义变量的数据类型是undefined】
（4）constructor属性：返回所有的JavaScript变量的构造函数
（5）JavaScript类型转化：使用JavaScript函数、通过JavaScript自身自动转换
a、数字转为字符串：全局方法String()、 Number方法toString();
b、布尔值转为字符串：全局方法String()、 Boolean方法toString();
c、日期转换为字符串：全局方法String()、 Date方法toString();
Date()方法：方法以及描述
getDate()：从Date对象中返回一个月中的某一天（1~31）
getDay()：从Date对象中返回一周的某一天（0~6）
getFullYear()：从Date对象以四位数字返回年份
getHours()：返回date对象的小时（0~23）
getMilliseconds()：返回date对象的毫秒（0~999）
getMinutes()：返回date对象的分钟（0~59）
getMonth()：返回date对象的月份（0~11）
getSeconds()：返回date对象的秒数（0~59）
getTime()：返回1970年1月1日至今的毫秒数
d、字符串转换为数字：全局方法Number()、parseFloat()、parseInt()、一元操作符+
e、布尔值转换为数字：全局方法Number()
f、日期转换为数字：全局方法Number()、日期方法getTime()
g、自动类型转化规则
（6）null：表示什么都没有，是只有一个值的特殊类型，表示一个空对象引用；当设置“null”时，可以用来清空对象；
（7）undefined：是指一个没有设置值的变量

23、JavaScript正则表达式（学习脑图）
（1）定义：使用单个字符串来描述、匹配一系列符合某个句法规则的字符串搜索模式
（2）字符串方法：
search()方法 用于检索字符串中指定的之字符串，或检索于正则表达式相匹配的子字符串，并返回字符串的起始位置；replace()方法 用于在字符串中用一些字符替换另一些字符，或替换一个与正则表达式匹配的子字符串；
（3）正则表达式修饰符：修饰符可以在全局搜索中不区分大小写；
修饰符以及描述：
i：执行对大小写不敏感的匹配；
g：执行全局匹配（查找所有的匹配，而非在找到第一个匹配后停止）；
m：执行多行匹配；
（4）正则表达式模式：方括号用于查找某个范围内的字符；
表达式以及描述：
[abc]：查找方括号之间的任何字符；
[0-9]：查找任何从0到9的数字；
(x|y)：查找任何以 | 分隔的选项；
元字符以及描述：
\d：查找数字;
\s：查找空白字符；
\uxxxx：查找以十六进制xxxx规定的Unicode字符；
量词以及描述：
n+：匹配任何包含至少一个n的字符串；
n-：匹配任何包含零个或多个n的字符串；
n?：匹配任何包含零个或一个n的字符串；

（5）test()方法用于检测一个字符串是否匹配某个模式，若字符串含有匹配的文本，返回true；
（6）exec()方法检索字符串中的正则表达式的匹配，该函数返回一个数组，存放匹配的结果，若没有匹配的，则返回值为null；
（7）compile()方法既可以改变检索模式，也可以添加或删除第二个参数；


24、JavaScript错误处理throw、try、catch
（1）try语句测试代码块的错误，catch语句处理错误，throw语句创建自定义错误，或抛出异常；

25、JavaScript调试
（1）浏览器中，点F12，console.log()方法进行调试；
（2）调试窗口中设置JavaScript断点；
（3）debugger关键字；

26、JavaScript表单验证
（1）验证：表单数据是否为空，输入是否是一个正确的Email地址，日期输入正确，输入的内容类型......
（2）Email验证：检验输入的数据是否符合电子邮件的基本语法；

27、JavaScript保留关键字
（1）JavaScript保留关键字，JavaScript对象,属性和方法，Java保留关键字，windows保留关键字，HTML事件句柄，非标准JavaScript关键字；

28、JavaScript JSON（JavaScript Object Notation）
（1）JSON用于存储和传输数据的格式，一般用于服务器端向网页传递数据，是一种轻量级数据交换格式；
（2）JSON语法规则：数据为键值对，数据有逗号分隔，大括号保留对象，中括号保留数组；
例：{"employees":[
            {"firstName": "john", "lastName": "Dow"},
            {"firstName": "Anna", "lastName": "Smith"}
    ]}
（3）由于JSON数据格式和JavaScript对象语法相同，因而JSON字符串转换为JavaScript对象，首先创建JavaScript字符串，字符串为JSON格式数据，然后使用JavaScript内置函数JSON.parse()将字符串转换为Javascript对象

29、JavaScript：void(0)含义
（1）void操作符指定要计算一个表达式单数不返回值，因为void(0)计算为0，没有任何效果；
（2）href="#"和href="javascript:void(0)"区别：前者包含一个位置信息，默认的锚点是#top（网页的上端），后者表示一个死链接；

30、JavaScript代码规范
（1)代码规范包括以下方面：变量和函数的命名规则，空格,缩进,注释的使用规则，其他规范......
（2）空格与运算符：加空格；代码缩进：4个空格符（少用tab键）；语句规则：分号结尾；函数；循环；条件语句；对象规则；命名规则；HTML载入外部JavaScript文件：只需要src属性；文件扩展名；


JS函数
31、JavaScript函数定义
（1）JavaScript关键字function定义函数，方式有：
函数声明：function Name(){code;}//声明后不会立刻执行，需要时调用；
函数表达式：例 var x= function (a, b){return a*b;}；
匿名函数：function(){code; }
立执行函数：(function(){code; }) ();
（2）Function()构造函数：例  var myFun= function(a, b) {return a* b;} var x= myFun(3, 4);
（3）函数可以在声明前调用，JavaScript特殊的机制；
（4）函数也是对象，JavaScript中使用typeof操作符判断函数类型，返回function；JavaScript函数的属性和方法：argument.length属性返回函数调用过程接收到的参数个数，toString()方法将函数作为一个字符串返回。

32、JavaScript函数参数
（1）参数规则：JavaScript定义参数时没有指定数据类型，JavaScript对隐藏参数（arguments）没有进行检测（包括个数）；
（2）函数调用时缺少参数，默认参数为undefined；
（3）JavaScript函数有内置对象arguments对象，该对象包含函数调用的参数数组；
（4）通过值传递参数，即在函数内部改变了变量的值，没有return出去时，函数外的改变量值不变；
（5）通过对象传递参数，在函数内部修改对象的属性就会修改其初始的值（对象可以理解为是一个指针）；

33、JavaScript函数调用
（1）this关键字：this指向函数执行的的当前对象；
（2）在html中默认的全局对象是HTML页面本身，所以函数属于HTML页面；在浏览器中的页面对象时浏览器对象（window对象），因为全局范围内定义的函数为window对象的函数；
（3）函数作为方法调用：将函数定义为对象的方法，例
var myObj= {
            firstName: "john", 
            lastName: "Doe", 
            fullName: function(){
                return this.firstName+ "  " + this.lastName;
                }
            }
myObj.fullName();//返回 "john  Doe"
（4）使用构造函数调用函数：使new关键字;构造函数调用会创建一个新的对象，新的对象会继承构造函数的属性和方法；
（5）使用函数方法调用函数：call()，apply()方法；两个方法可用于调用函数，两个方法的第一个参数必须是对象本身，而apply()方法第二个参数传入一个参数数组（多个参数组合而成），call()方法则是一个个参数传入；通过call()和apply()方法可以设置this的值，作为已存在对象的新方法调用；

34、JavaScript闭包
（1）JavaScript变量：局部变量，全局变量；
（2）变量生命周期：局部变量为函数内部作用域；全局变量为全局作用域；
（3）计数器：使用全局变量[注意return的使用，是否需要返回值]
（4）JavaScript内嵌函数
（5）JavaScript闭包：可以访问上一层函数作用域里变量的函数，即上一层函数已经关闭；本质上，闭包就是将函数内部和函数外部联系起来的桥梁；【注意：闭包会使得函数的变量保存在内存中，对内存消耗大；闭包会在父函数外部，改变父函数内部变量的值】；


JS HTML DOM
35、HTML DOM（学习脑图）
（1）通过HTML DOM，可以访问JavaScript HTML 文档的所有元素；
（2）通过可编程对象模型，JavaScript能够改变页面中所有的HTML元素，HTML属性，CSS样式，能对页面所有的事件做出反应；
（3）查找HTML元素：
ID查找html元素【document.getElementById("ID名")】，
标签名查找html元素【document.getElementsByTagName("p")】，
类名查找html元素【document.getElementsByClassName("Class类名")】；

36、HTMLDOM改变HTNL内容
（1）改变HTML输出流：例 document.write(Date());
（2）改变HTML内容：
语法：document.getElementById(id).innerHTML= new HTML;
例：document.getElementById("name").innerHTML= "new TEXT";
（3）改变HTML属性：document.getElementById(id).attribute= new value;
例：document.getElementById("image").src= "icon.png";

37、HTML DOM改变CSS
（1）改变HTML样式：
语法：document.getElementById(id).style.property= new style;
例：document.getElementById("style").style.color= "blue";

38、HTML DOM事件：对HTTML事件做出反应
（1）HTML事件：
按下鼠标按钮时onmousedown，释放鼠标按钮时onmouseup，完成点击鼠标时：onclick
用户进入或者离开页面：onload，onunload
网页加载时：
图像加载时：
鼠标移动到元素上或者移出元素时：onmouseover，onmouseout
输入字段改变时：onchange
输入字段获取焦点时：onfocus
提交HTML表单时：
用户触发按钮时：

39、HTML DOM EventListener
（1）addEventListener()方法：用于向指定元素添加事件句柄（添加的事件句柄不会覆盖已存在的事件句柄）；可以简单的控制事件（冒泡与捕获）；
removeEventListener()移出事件的监听；
语法：element.addEventListener(event, function, useCapture);//第一个参数是事件的类型，第二个时事件触发后调用的函数，第三个参数是Boolean值，描述事件是冒泡还是捕获。【注意不要使用”on“前缀】
（2）向原元素添加事件句柄；向同一个元素添加多个事件句柄；向同一个元素添加不同类型事件；向window对象添加事件句柄；传递参数（使用”匿名函数“调用带参数的函数），例 element.addEventListener("click", function(){ myFun(p1, p2); } )

40、HTML DOM元素
（1）节点三个重要属性：nodeName（节点名称），nodeValue（节点值），nodeType（节点类型）
（2）创建新的HTML元素步骤：先创建该元素document.creatElement()（元素节点），为其添加一定内容document.creatTextNode()，向一个已存在的元素追加该元素，例 element.appendChild() 。
（3）删除已有的HTML元素：element.removeChild();//删除子节点所有元素

JS高级教程
41、JavaScript对象
（1）JavaScript所有的食物都是对象（布尔型、数字型、字符串、日期、数学和正则表达式、数值、函数......），也可以自定义对象；
（2）对象只是一种特殊的数据，拥有属性和方法；访问对象的属性和方法的语法：objectName.propertyName/ objectName.methodName()
（3）创建JavaScript对象，方法：定义并创建对象的实例；使用函数来定义对象，然后创建对象的实例；
（4）JavaScript是面向对象的语言，基于原型链prototype属性；
（5）for-in语句遍历对象的属性；


42、JavaScript Number对象
（1）JavaScriptNumber对象是经过封装的，能让你处理数字的对象，由Number()构造器创建，JavaScript只有一中数字类型；
（2）JavaScript数字均为64位；无穷大（Infinity）；NaN（非数字值）；
（3）数字属性：MAX_VALUE、MIN_VALUE、NEGATIVE_INFINITY、POSIITIVE_INFINITY、NaN、prototype、constructor
数字方法：toExponential()、toFixed()、toPrecision()、toString()、valueOf()

43、JavaScript String（字符串）对象：处理已有的字符块
（1）JavaScript字符串用于存储一些列字符；字符串可以使用单引号或双引号；使用索引访问字符串中任何的字符（索引从0开始）；字符串中特殊符号使用转义字符（\）转义使用；
（2）计算字符串长度使用长度属性 length；
（3）字符串使用 indecOf() 方法来定位字符串中某一个指定字符首次出现的位置； 
（4）字符串使用 match() 方法查找字符串中特定的字符，找到则返回该字符；
（5）字符串使用 replace() 方法替换一些字符；
（6）字符串大小写转换使用函数 toUpperCase() / toLowerCase()；
（7）字符串使用 split()  方法转为数组；
（8）JavaScript中可以使用转义字符（\）插入特殊符号；例：\'    \"    \\    \n 换行    \r 回车    \t tab键    \f 换页
（9）字符串属性和方法：
属性：length、prototype、constructor
方法：charAt()、charCodeAt()、concat()、fromCharCode、indexOf()、lastIndexOf()、match()、replace()、search()、slice()、split()、substr()、substring()、toLowerCase()、toUpperCase()、valueOf()

44、JavaScript Date（日期）对象：处理时间和日期
（1）date对象属性：constructor、prototype
（2）Date对象方法：
get/setDate():一个月中的某一天1-31；
getDay():一周中的某一天0-6；
get/setFullYear():四位数的年份；
get/setHours():小时0-23;
get/setMilliseconds():毫秒0-999;
get/setMinutes():分钟0-59;
get/setMonth():月份0-11；
get/setSeconds():秒数0-59；
get/setTime():1970-1-1至今的毫秒数；
getTimezoneOffset():返回本地时间与格林威治时间的分钟差；
get/setUTCDate():根据世界时返回月中的某一天
getUTCDay():
get/setUTCFullYear():
get/setUTCHours():
get/setUTCMilliseconds():
get/setUTCMinutes():
ge/settUTCMonth():
get/setUTCSeconds():
parse()：1970-1-1至指定日期（字符串）的毫秒数；
toDateString():把日期部分换为字符串；
toISOString():以ISO标准返回字符串日期格式；
toJSON():以JSON数据格式返回字符串日期格式；
toLocalDateString():根据本地时间格式，将Date对象的日期部分转换为字符串；
toLocalTimeString():根据本地时间格式，将Date对象的时间部分转换为字符串；
toLocalString():根据本地时间格式，将Date对象转换为字符串；
toString():把Date对象转换为字符串；
toTimeString():把Date对象的时间部分转换为字符串；
toUTCString():根据世界时，把Date对象转换为字符串；
UTC():根据世界时间返回1970-1-1到指定日期的毫秒数；
valueOf():返回Date对象的原始值；

45、JavaScript Array（数组）对象：使用单独的变量名来储存一些列的值；（学习脑图）
（1）创建数组：
常规方式 例 var myStr= new Array(); //再填入值就行
简洁方式 例 var myStr= new Array("name", "age", "work");
字面量 例 var myStr= ["name", "age", "work"];
（2）访问数组：通过指定数组名以及索引号码，可以访问某个特定元素；
（3）Array对象方法：
concat():连接两个或更多数组，返回结果；
every():检测数组元素的每个元素是否都符合条件；
filter():检测数组元素，返回符合条件所有元素的数组；
indexOf():搜索数组中的元素，返会它所在的位置；
join():把数组的所有元素放入一个字符串；
lastIndexOf():返回一个指定字符串值最后出现的位置，在一个字符串中指定位置从后向前搜索；
map():通过指定函数处理数组的每一个元素，并返回处理后的数组；
pop():删除数组的最后一个元素并返回删除的元素；
push():向数组的末尾添加一个或更多元素，并返回新的数组；
reverse():反转数组的元素顺序；
shift():删除并返回数组的第一个元素；
slice():选取数组的一部分，返回一个新数组；
some():检测数组元素中是否有元素符合指定条件；
sort():对数组元素进行排序；
splice():从数组中添加或删除元素；
toString():把数组转换为字符串，并返回结果；
unshift():向数组的开头添加一个或更多元素，并返回新的数组；
valueOf():返回数组对象的原始值；

46、JavaScript Boolean（布尔）对象：将非布尔值转换为布尔值
（1）创建Boolean对象，var myBool= new Boolean();
（2）Boolean对象属性和方法：
constructor，prototype；
toString() , valueOf();

47、JavaScript Math（算数）对象:执行常见的算数任务
（1)Math 对象属性
E:返回算术常量e，即自然对数的底数（约为2.718）；
LN2:返回2的自然对数（约为0.693）；
LN10:返回10的自然对数（约为2.302）；
LOG2E:返回以2为底的e的对数（约为1.414）；
LOG10E:返回以10为底的e的对数（约为0.434）；
PI:返回圆周率，（约为3.14159）；
SQRT1_2:返回2的平方根的倒数（约为0.707）；
SQRT2:返回2的平方根（约为1.414）；
（2）Math对象方法
abs(x):绝对值
acos(x):反余弦
asin(x):反正弦
atan2(y, x):返回从x周到点（x， y）的角度（-90°到90°）
ceil(x):对数进行向上取整
cos(x):余弦
exp(x):返回E的x次方的指数
floor(x):对x进行向下取整
log(x):数的自然对数
max(x, y, z,.....):返回最大值
min(x, y, z,.....):返回最小值
pow(x, y):返回x的y次幂
random():返回0-1的随机数
round():数的四舍五入
sin(x):正弦
sqrt(x):数的平方跟
tan(x):正切

48、JavaScript RegExp对象：规定在文本中检索的内容
（1）

49、JavaScript Window对象

50、JavaScript execCommand函数

JS浏览器BOM
51、JavaScript Window

52、JavaScript Window Screen

53、JavaScript Window Location

54、JavaScript Window History

55、JavaScript Window Navigator

56、JavaScript 弹窗

57、JavaScript计时事件

58、JavaScript Cookies

JS库
59、JavaScript 库

60、 JavaScript 测试JQuery

61、JavaScript 测试Prototype

JS实例
62、JavaScript 实例

63、JavaScript 对象实例

64、JavaScript浏览器对象实例

65、JavaScript HTML DOM 实例

66、JavaScript 总结

67、JavaScript 测试

68、JavaScript编程实战闯关

```















