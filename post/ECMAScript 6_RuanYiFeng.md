---
title: "ECMAScript 6学习笔记"
date: 2018-07-26T00:00:03+08:00
draft: true
---
# ECMAScript 6  


1、ECMAScript简介
（1）ECMAScript与JavaScript关系是，前者时后者的规格，后者是前者的一种实现；
（2）部署进度：查看浏览器支持ES6程度    $ npm inatall -g es-checker    $ es-checker
（3）Babel转码器：将ES6语法转为ES5语法
配置文件：.babelrc（略）
命令行转码：babel-cli 工具
全局环境下的操作：
安装命令：$ npm install  --global babel-cli
基本用法：
转码结果输出到标准输出：$ babel example.js
转码结果写入一个文件（--out-file 或者 -o 参数指定输出文件）：$ babel example.js -o compailed.js
整个目录转码（--out-dir 或者 -d 参数制定输出目录）：$ babel src -d lib
-s 参数生成 source map 文件：$ babel src -d lib -s

直接安装 babel-cli 在项目中：
安装命令：$ npm install --save-dev babel-cli
改写 package.json 文件：加入  "scripts": { "build" : " babel src -d -lib"},
转码时，执行下面命令： $ npm run build

babel-node:该命令提供一个支持ES6的REPL环境，随着 babel-cli 一起安装，执行 babel-node 就进入REPL环境；也可以直接安装在项目中    $ npm install --save-dev babel-cli
在改写 package.json 文件，"scripts" : { " scripts-name" : " babel-node scripts.js" }
就可用babel-node 取代node，scripts.js 文件不用做任何转码处理。

babel-register：该模块改写 require 命令， 为它加一个钩子，每当用 require 加载.js/.jsx/.es/.es6后缀名文件时，就会先用babel转码。
安装命令：    $ npm install --save-dev babel-register    
在使用前必须先加载babel-register：    require("babel-register");require("xxx.js");

babel-core 模块：调用babel的API进行转码

babel-polyfill:

浏览器环境：

Babel在线转换：

与其他工具配合：ESlint和Mocha

（4）Traceur转码器：

2、let和const命令
（1）let命令基本语法：
let声明变量：只在let 命令所在的代码块内有效（区别于var 声明变量，在全局作用域有效）；
不存在变量的提升：例 var命令会发生”变量提升“现象，var声明的变量可以在声明前使用，而let 命令所声明的变量一定在声明后才可以使用；
暂时性死区：只要在块级作用域内存在 let 和 const 命令，它所声明的变量就“绑定”这个区域，不再受外部的的影响；（即这个区块形成了封闭的作用域，变量声明后才能使用）同时，typeof 方法对于用let 命令所声明的变量前使用的话，也会报错；
不允许重复声明：相同的作用域内，只允许声明一次；
（2）块级作用域：
ES5中只具有函数作用域以及全局作用域，存在一定问题，例内存变量可能会覆盖外层变量；用来计数的循环变量泄露为全局变量；
ES6块级作用域实际就是let 命令的作用，块级作用域可以任意嵌套，块级作用域的出现运用取代了原有的立执行函数表达式（IIFE）的运用；
块级作用域与函数声明：ES5规定函数只能在顶层作用域和函数作用域中声明，不能再块级作用域中声明，因而函数在if()语句/try{}中定义就不正确；ES6明确允许块级作用域中声明函数，块级作用域中函数声明类似与 let ，在块级作用域外不可引用；【避免在块级作用域里面声明函数，若确实需要，应写成函数表达式】

（3）const 命令：声明一个只读的常量，声明后值不能改变
const 的作用域与let 命令相同，只在声明所在的块级作用域有效；const 命令声明的常量也不可提升，存在暂时性死区，只能在声明后使用，也不可重复声明；
const的本质是变量指向的那个内存地址所保留的数据不得改动，对于简单数据类型（数值，字符串，布尔值），值就保存在变量所指向的那个内存地址，等同于常量；而对于复杂数据类型（主要是对象和数组），变量指向的是内存地址，保存的只是一个实际数据的指针，因而，const 只能保证这个指针是固定指向某一地址，至于它指向的数据结构是不是可变，就不能控制了，因而，对象声明为常量必须非常小心。
对象冻结：Object.freeze() 方法；
ES6变量声明的六种方法：（ES5）var，function，（ES6新增）let，const，import，class；

（4）顶层对象的属性：浏览器环境为 window 对象，Node中是 global 对象，ES5中，顶层对象的属性和全局变量是等价的；
所带来的问题：无法在编译时就报错，顶层对象属性可到处读写；ES6中保持兼容性，var和function命令申明的依旧是顶层对象属性，而let,const,class为全局变量，不属于顶层对象属性；


3、变量的解构赋值
（1）基本用法：ES6允许按照一定模式，从数组和对象中提取值，对变量进行赋值；
例 let [a, b, c]= [1, 3, 5];//这种写法本质上属于“模式匹配”
（2）对于set结构，可以使用数组的解构赋值；例 let [x, y, z]= new Set( [ 'a', 'b', 'c' ]);
【只要数据结构具有Irerator 接口， 就能采用数组形式的解构赋值】
（3）对象的解构赋值：对象时以属性名匹配来取值的，而之前的数组是以元素的排序来对取值的；【注意赋值的变量与匹配模式变量的区别，可以嵌套赋值】
（4）字符串的解构赋值：字符串被转换成了一个类是数组的对象；
（5）数值与布尔值的解构赋值：先转对象，再赋值；
（6）函数参数的解构赋值：
（7）圆括号问题：只要有可能导致解构的歧义，就不得使用圆括号；
不能使用圆括号情况：变量声明语句，函数参数，赋值语句模式；
（8）用途：交换变量的值，从函数返回值，参数的定义，提取JSON数据，函数参数的默认值，遍历Map结构（for of 循环遍历），输入模块的指定方法；

4、字符串的扩展
（1）字符的Unicode表示法：JavaScript允许采用 \uxxxx 形式表示一个字符，其中xxxx 表示字符的Unicode码点；
（2）codePointAt()：JavaScript内部，字符以UTF-16的格式存储，每个字符固定为2哥字节，但对于那些需要4个字节的（Unicode码点大于0xFFFF的字符），JavaScript会认为它是两个字符；ES5中charAt()方法无法读取整个字符，charCodeAt()方法只能分别返回前两个字节和后两个字节的值；
而ES6提供 codePointAt()方法，能正确处理4个字节存储的字符，返回一个字符的码点；codePointAt()方法的参数是字符在字符串中的位置（从0开始），返回的码点是十进制值，若想要16进制值，使用 toString() 方法转换；
（3）String.fromCodePoint()方法：用于从码点返回对应字符；
由于ES5中的String.fromCharPoint()方法不能识别32位的UTF-16字符（Unicode编号大于 0xFFFF），会自动舍弃最高位的数；
而ES6中提出的String.fromCodePoint()用于从码点返回对应字符，作用与codePointAt()方法相反；
（4）字符串的遍历器接口：ES6为字符串添加了遍历器接口（lterator章节），使得字符串可以被 for...of 循环遍历；（该遍历器可识别大于0xFFFF 的码点）
（5）at()方法：ES5中所提供的charAt() 方法，返回字符串给定位置的字符，但是该方法不能识别码点大于0xFFFF的字符；而at()方法可以识别码点大于0xFFFF的字符，返回正确的字符；
（6）normalize()方法：用于将字符的不同表示方法统一为同样的形式，这成为Unicode正规化；该方法参数有 NFC（默认，返回多个简单字符的合成字符）、NFD（返回合成字符分解的多个简单字符）;
（7）确定一个字符串是否包含与另一个字符串中，传统JavaScript用 indexOf()方法，ES6提供了三种新方法：（第一个参数必填，第二个参数可选，表示开始搜索的位置）
includes()：返回布尔值，表示是否找到参数字符串；
startsWith()：返回布尔值，表示参数字符串是否在原字符串的头部；
endsWith()：返回布尔值，表示参数字符串是否在原字符串的尾部；
（8）repeat()方法返回一个新的字符串，表示将原字符串重复 n 次；（参数为重复次数）
（9）ES2017 引入了字符串补全长度的功能，若某个字符串不够指定长度，会在头部和尾部补全，padStart()方法用于头部补全，padEnd()方法用于尾部补全，两个参数，第一个参数用来指定字符串的最小长度，第二个参数用来补全字符串，省略第二参数就会用空格补全；
（10）matchAll()方法：返回一个正则表达式在当前字符串的所有匹配；
（11）模板字符串：用反引号( ` )标识【位于tab键上方】，可当作普通字符串使用，也可以来定义多行字符串，或者在字符串中潜嵌入变量；可以用trim()方法消除模板字符串中的空格和换行；模板字符串中嵌入变量，需将变量名写在  ${ }  中，大括号内可以放入JavaScript表达式，可以进行运算，以及引用对象的属性，还可以调用函数；
（12）实例：模板编译？未看懂
该模板使用<%...%>放置JavaScript代码，<%=...%>输出JavaScript表达式；
（13）标签模板：模板字符串还可以跟在一个函数后面，该函数将被调用来处理这个模板字符串，若模板字符串中有变量，会见模板字符串先处理成多个参数，在调用函数；
标签模板 的一个重要应用激素过滤HTML字符串，防止用户输入恶意内容；
（14）String.raw()方法：可以作为处理模板字符串的基本方法，它会将所有的变量替换，而且对斜杠进行转义，方便下一步作为字符串使用；
（15）模块字符串的限制：由于模块字符串默认会将字符串转义，导致无法嵌入其他语言；


5、正则的扩展
（1）RegExp 构造函数：
ES5中，其参数有两种情况：第一种情况是，参数是字符串，这时第二个参数表示正则表达式的修饰符（flag）；第二种情况是，参数是一个正则表示式，这时会返回一个原有正则表达式的拷贝。
（2）字符串的正则方法：
字符串对象共有 4 个方法，可以使用正则表达式：match()、replace()、search()和split()；
ES6 将这 4 个方法，在语言内部全部调用RegExp的实例方法，从而做到所有与正则相关的方法，全都定义在RegExp对象上。
* String.prototype.match 调用 RegExp.prototype[Symbol.match]
* String.prototype.replace 调用 RegExp.prototype[Symbol.replace]
* String.prototype.search 调用 RegExp.prototype[Symbol.search]
* String.prototype.split 调用 RegExp.prototype[Symbol.split]
（3）u 修饰符：
ES6 对正则表达式添加了u修饰符，用来正确处理大于\uFFFF的 Unicode 字符。也就是说，会正确处理四个字节的 UTF-16 编码
（3-1） 点（.）字符：在正则表达式中，含义是除了换行符以外的任意单个字符。对于码点大于0xFFFF的 Unicode 字符，点字符不能识别，必须加上u修饰符。例： 
var s = '𠮷';
/^.$/.test(s) // false   
/^.$/u.test(s) // true
（3-2） Unicode 字符表示法：ES6 新增了使用大括号表示 Unicode 字符，这种表示法在正则表达式中必须加上u修饰符，才能识别当中的大括号，否则会被解读为量词；例：
/\u{61}/.test('a') // false
/\u{61}/u.test('a') // true
/\u{20BB7}/u.test('𠮷') // true
（3-3） 量词
使用u修饰符后，所有量词都会正确识别码点大于0xFFFF的 Unicode 字符；例： 
/a{2}/.test('aa') // true
/a{2}/u.test('aa') // true
/𠮷{2}/.test('𠮷𠮷') // false
/𠮷{2}/u.test('𠮷𠮷') // true
（3-4）预定义模式
u修饰符也影响到预定义模式，能否正确识别码点大于0xFFFF的 Unicode 字符；例：
/^\S$/.test('𠮷') // false
/^\S$/u.test('𠮷') // true
（3-5）i 修饰符
有些 Unicode 字符的编码不同，但是字型很相近，比如，\u004B与\u212A都是大写的K。
（4）RegExp.prototype.unicode 属性
正则实例对象新增unicode属性，表示是否设置了u修饰符。例：
const r1 = /hello/;
const r2 = /hello/u;
r1.unicode // false
r2.unicode // true
（5）y 修饰符
ES6 还为正则表达式添加了y修饰符，叫做“粘连”（sticky）修饰符，y修饰符的作用与g修饰符类似，也是全局匹配，后一次匹配都从上一次匹配成功的下一个位置开始。不同之处在于，g修饰符只要剩余位置中存在匹配就可，而y修饰符确保匹配必须从剩余的第一个位置开始，这也就是“粘连”的涵义
（6）RegExp.prototype.sticky 属性
与y修饰符相匹配，ES6 的正则实例对象多了sticky属性，表示是否设置了y修饰符。例：
var r = /hello\d/y;
r.sticky // true
（7）RegExp.prototype.flags 属性
ES6 为正则表达式新增了flags属性，会返回正则表达式的修饰符；例
// ES5 的 source 属性，返回正则表达式的正文
/abc/ig.source        // "abc"
// ES6 的 flags 属性，返回正则表达式的修饰符
/abc/ig.flags        // 'gi'
（8）s 修饰符：dotAll 模式
正则表达式中，点（.）是一个特殊字符，代表任意的单个字符，但是有两个例外。一个是四个字节的 UTF-16 字符，这个可以用u修饰符解决；另一个是行终止符（line terminator character）。
以下四个字符属于”行终止符“。
* U+000A 换行符（\n）
* U+000D 回车符（\r）
* U+2028 行分隔符（line separator）
* U+2029 段分隔符（paragraph separator）
例：
/foo.bar/.test('foo\nbar')            // false
/foo[^]bar/.test('foo\nbar')        // true
ES2018 引入s修饰符，使得.可以匹配任意单个字符。
/foo.bar/s.test('foo\nbar')          // true
这被称为dotAll模式，即点（dot）代表一切字符。所以，正则表达式还引入了一个dotAll属性，返回一个布尔值，表示该正则表达式是否处在dotAll模式。
（9）后行断言(没怎么看懂）
”先行断言“指的是，x只有在y前面才匹配，必须写成/x(?=y)/。比如，只匹配百分号之前的数字，要写成/\d+(?=%)/。”先行否定断言“指的是，x只有不在y前面才匹配，必须写成/x(?!y)/。比如，只匹配不在百分号之前的数字，要写成/\d+(?!%)/；例：
/\d+(?=%)/.exec('100% of US presidents have been male')  // ["100"]
/\d+(?!%)/.exec('that’s all 44 of them')                                 // ["44"]

“后行断言”正好与“先行断言”相反，x只有在y后面才匹配，必须写成/(?<=y)x/。比如，只匹配美元符号之后的数字，要写成/(?<=\$)\d+/。”后行否定断言“则与”先行否定断言“相反，x只有不在y后面才匹配，必须写成
/(?<!y)x/。比如，只匹配不在美元符号后面的数字，要写成/(?<!\$)\d+/;

（10）Unicode 属性类
ES2018 引入了一种新的类的写法\p{...}和\P{...}，允许正则表达式匹配符合 Unicode 某种属性的所有字符；例：
const regexGreekSymbol = /\p{Script=Greek}/u;
regexGreekSymbol.test('π') // true

Unicode 属性类要指定属性名和属性值，语法：\p{UnicodePropertyName=UnicodePropertyValue}

对于某些属性，可以只写属性名，或者只写属性值。
下面是其他一些例子：
// 匹配所有空格
\p{White_Space}

// 匹配各种文字的所有字母，等同于 Unicode 版的 \w
[\p{Alphabetic}\p{Mark}\p{Decimal_Number}\p{Connector_Punctuation}\p{Join_Control}]

// 匹配各种文字的所有非字母的字符，等同于 Unicode 版的 \W
[^\p{Alphabetic}\p{Mark}\p{Decimal_Number}\p{Connector_Punctuation}\p{Join_Control}]

// 匹配 Emoji
/\p{Emoji_Modifier_Base}\p{Emoji_Modifier}?|\p{Emoji_Presentation}|\p{Emoji}\uFE0F/gu

// 匹配所有的箭头字符
const regexArrows = /^\p{Block=Arrows}+$/u;
regexArrows.test('←↑→↓↔↕↖↗↘↙⇏⇐⇑⇒⇓⇔⇕⇖⇗⇘⇙⇧⇩') // true

（11）具名组匹配：正则表达式使用圆括号进行组匹配；
ES2018 引入了具名组匹配（Named Capture Groups），允许为每一个组匹配指定一个名字，既便于阅读代码，又便于引用。例：
const RE_DATE = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/;
const matchObj = RE_DATE.exec('1999-12-31');
const year = matchObj.groups.year;             // 1999
const month = matchObj.groups.month;     // 12
const day = matchObj.groups.day;               // 31

（11-1）解构赋值和替换
有了具名组匹配以后，可以使用解构赋值直接从匹配结果上为变量赋值，例 ；
let {groups: {one, two}} = /^(?<one>.*):(?<two>.*)$/u.exec('foo:bar');
one  // foo
two  // bar

字符串替换时，使用$<组名>引用具名组，例：
let re = /(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})/u;
'2015-01-02'.replace(re, '$<day>/$<month>/$<year>')        // '02/01/2015'

（11-2）引用（未看懂）
如果要在正则表达式内部引用某个“具名组匹配”，可以使用\k<组名>的写法；例：
const RE_TWICE = /^(?<word>[a-z]+)!\k<word>$/;
RE_TWICE.test('abc!abc') // true
RE_TWICE.test('abc!ab') // false
数字引用（\1）依然有效，例：
const RE_TWICE = /^(?<word>[a-z]+)!\1$/;
RE_TWICE.test('abc!abc') // true
RE_TWICE.test('abc!ab') // false

（12）String.prototype.matchAll
如果一个正则表达式在字符串里面有多个匹配，现在一般使用g修饰符或y修饰符，在循环里面逐一取出，例：
var regex = /t(e)(st(\d?))/g;var string = 'test1test2test3';
var matches = [];var match;while (match = regex.exec(string)) {
  matches.push(match);}
matches
// [
//   ["test1", "e", "st1", "1", index: 0, input: "test1test2test3"],
//   ["test2", "e", "st2", "2", index: 5, input: "test1test2test3"],
//   ["test3", "e", "st3", "3", index: 10, input: "test1test2test3"]
// ]

目前有一个提案，增加了String.prototype.matchAll方法，可以一次性取出所有匹配。不过，它返回的是一个遍历器（Iterator），而不是数组；由于string.matchAll(regex)返回的是遍历器，所以可以用for...of循环取出。相对于返回数组，返回遍历器的好处在于，如果匹配结果是一个很大的数组，那么遍历器比较节省资源；遍历器转为数组是非常简单的，使用 ... 运算符和Array.from方法就可以了。

6、数值的扩展
（1）二进制和八进制表示法：
ES6 提供了二进制和八进制数值的新的写法，分别用前缀0b（或0B）和0o（或0O）表示；
如果要将0b和0o前缀的字符串数值转为十进制，要使用Number方法，例：
Number('0b111')  // 7
Number('0o10')  // 8

（2）Number.isFinite(), Number.isNaN()
Number.isFinite() 用来检查一个数值是否为有限的（finite），即不是Infinity；注意，如果参数类型不是数值，Number.isFinite一律返回false。
Number.isNaN() 用来检查一个值是否为NaN，如果参数类型不是NaN，Number.isNaN一律返回false；
它们与传统的全局方法isFinite()和isNaN()的区别在于，传统方法先调用Number()将非数值的值转为数值，再进行判断，而这两个新方法只对数值有效，Number.isFinite()对于非数值一律返回false, Number.isNaN()只有对于NaN才返回true，非NaN一律返回false

（3）Number.parseInt(), Number.parseFloat()
ES6 将全局方法parseInt()和parseFloat()，移植到Number对象上面，行为完全保持不变，目的是逐步减少全局性方法，使得语言逐步模块化。

（4）Number.isInteger()：用来判断一个数值是否为整数
JavaScript 内部，整数和浮点数采用的是同样的储存方法，所以 25 和 25.0 被视为同一个值，例：
Number.isInteger(25) // true
Number.isInteger(25.0) // true

如果参数不是数值，Number.isInteger返回false；
注意，由于 JavaScript 采用 IEEE 754 标准，数值存储为64位双精度格式，数值精度最多可以达到 53 个二进制位（1 个隐藏位与 52 个有效位）。如果数值的精度超过这个限度，第54位及后面的位就会被丢弃，这种情况下，Number.isInteger可能会误判，原因就是这个小数的精度达到了小数点后16个十进制位，转成二进制位超过了53个二进制位，导致最后的数被丢弃了。

（5）Number.EPSILON
ES6 在Number对象上面，新增一个极小的常量Number.EPSILON。根据规格，它表示 1 与大于 1 的最小浮点数之间的差；对于 64 位浮点数来说，大于 1 的最小浮点数相当于二进制的1.00..001，小数点后面有连续 51 个零。这个值减去 1 之后，就等于 2 的 -52 次方，例：
Number.EPSILON === Math.pow(2, -52)            // true

Number.EPSILON可以用来设置“能够接受的误差范围”；比如，误差范围设为 2 的-50 次方（即Number.EPSILON * Math.pow(2, 2)），即如果两个浮点数的差小于这个值，我们就认为这两个浮点数相等。因此，Number.EPSILON的实质是一个可以接受的最小误差范围。例：//为浮点数运算，部署了一个误差检查函数
function withinErrorMargin (left, right) {
  return Math.abs(left - right) < Number.EPSILON * Math.pow(2, 2);}
0.1 + 0.2 === 0.3 // false
withinErrorMargin(0.1 + 0.2, 0.3) // true
1.1 + 1.3 === 2.4 // false
withinErrorMargin(1.1 + 1.3, 2.4) // true

(6）安全整数和 Number.isSafeInteger()
JavaScript 能够准确表示的整数范围在-2^53到2^53之间（不含两个端点），超过这个范围，无法精确表示这个值。ES6 引入了Number.MAX_SAFE_INTEGER和Number.MIN_SAFE_INTEGER这两个常量，用来表示这个范围的上下限。

Number.MAX_SAFE_INTEGER === Math.pow(2, 53) - 1                        // true
Number.MAX_SAFE_INTEGER === 9007199254740991                        // true
Number.MIN_SAFE_INTEGER === -Number.MAX_SAFE_INTEGER       // true
Number.MIN_SAFE_INTEGER === -9007199254740991                        // true

Number.isSafeInteger()：用来判断一个整数是否落在这个范围之内；该函数的实现：
Number.isSafeInteger = function (n) {
  return (typeof n === 'number' &&
    Math.round(n) === n &&
    Number.MIN_SAFE_INTEGER <= n &&
    n <= Number.MAX_SAFE_INTEGER);}

实际使用这个函数时，需要注意。验证运算结果是否落在安全整数的范围内，不要只验证运算结果，而要同时验证参与运算的每个值。所以，如果只验证运算结果是否为安全整数，很可能得到错误结果。下面的函数可以同时验证两个运算数和运算结果：
function trusty (left, right, result) {
  if (
    Number.isSafeInteger(left) &&
    Number.isSafeInteger(right) &&
    Number.isSafeInteger(result)
  ) {
    return result;
  }
  throw new RangeError('Operation cannot be trusted!');}
trusty(9007199254740993, 990, 9007199254740993 - 990)
// RangeError: Operation cannot be trusted!
trusty(1, 2, 3)         // 3

（7）Math 对象的扩展
ES6 在 Math 对象上新增了 17 个与数学相关的方法。所有这些方法都是静态方法，只能在 Math 对象上调用。

Math.trunc()方法：用于去除一个数的小数部分，返回整数部分。对于非数值，Math.trunc内部使用Number方法将其先转为数值；对于空值和无法截取整数的值，返回NaN；对于没有部署这个方法的环境，可以用下面的代码模拟：
Math.trunc = Math.trunc || function(x) { return x < 0 ? Math.ceil(x) : Math.floor(x);};

Math.sign()方法：用来判断一个数到底是正数、负数、还是零。对于非数值，会先将其转换为数值。
它会返回五种值：* 参数为正数，返回+1；* 参数为负数，返回-1；* 参数为 0，返回0；* 参数为-0，返回-0;* 其他值，返回NaN。对于没有部署这个方法的环境，可以用下面的代码模拟：
Math.sign = Math.sign || function(x) {
  x = +x;         // convert to a number
  if (x === 0 || isNaN(x)) {
    return x;
  }
  return x > 0 ? 1 : -1;};

Math.cbrt()方法：用于计算一个数的立方根。
对于非数值，Math.cbrt方法内部也是先使用Number方法将其转为数值；对于没有部署这个方法的环境，可以用下面的代码模拟：
Math.cbrt = Math.cbrt || function(x) {
  var y = Math.pow(Math.abs(x), 1/3);
  return x < 0 ? -y : y;};

Math.clz32()方法：由于JavaScript 的整数使用 32 位二进制形式表示，因此该方法返回一个数的 32 位无符号整数形式有多少个前导 0；
左移运算符（<<）与Math.clz32方法直接相关；对于小数，Math.clz32方法只考虑整数部分；
对于空值或其他类型的值，Math.clz32方法会将它们先转为数值，然后再计算，例：
Math.clz32()                  // 32
Math.clz32(NaN)          // 32
Math.clz32(Infinity)     // 32
Math.clz32(null)           // 32
Math.clz32('foo')         // 32
Math.clz32([])              // 32
Math.clz32({})              // 32
Math.clz32(true)          // 31

Math.imul()方法：返回两个数以 32 位带符号整数形式相乘的结果，返回的也是一个 32 位的带符号整数。
之所以需要部署这个方法，是因为 JavaScript 有精度限制，超过 2 的 53 次方的值无法精确表示。这就是说，对于那些很大的数的乘法，低位数值往往都是不精确的，Math.imul方法可以返回正确的低位数值；

Math.fround()方法：返回一个数的32位单精度浮点数形式。
Math.fround方法的主要作用，是将64位双精度浮点数转为32位单精度浮点数。如果小数的精度超过24个二进制位，返回值就会不同于原值，否则返回值不变（即与64位双精度值一致）；对于 NaN 和 Infinity，此方法返回原值。对于其它类型的非数值，Math.fround 方法会先将其转为数值，再返回单精度浮点数；对于没有部署这个方法的环境，可以用下面的代码模拟：
Math.fround = Math.fround || function (x) {return new Float32Array([x])[0];};

Math.hypot()方法：返回所有参数的平方和的平方根。
如果参数不是数值，Math.hypot方法会将其转为数值。只要有一个参数无法转为数值，就会返回 NaN。

对数方法：ES6 新增了 4 个对数相关方法
Math.expm1()方法：返回 ex - 1，即Math.exp(x) - 1；
 
Math.log1p(x)方法：返回1 + x的自然对数，即Math.log(1 + x)。如果x小于-1，返回NaN。

Math.log10(x) 方法：返回以 10 为底的x的对数。如果x小于 0，则返回 NaN。

Math.log2(x) 方法：返回以 2 为底的x的对数。如果x小于 0，则返回 NaN。

双曲函数方法：ES6 新增了 6 个双曲函数方法
Math.sinh(x) 返回x的双曲正弦（hyperbolic sine）
Math.cosh(x) 返回x的双曲余弦（hyperbolic cosine）
Math.tanh(x) 返回x的双曲正切（hyperbolic tangent）
Math.asinh(x) 返回x的反双曲正弦（inverse hyperbolic sine）
Math.acosh(x) 返回x的反双曲余弦（inverse hyperbolic cosine）
Math.atanh(x) 返回x的反双曲正切（inverse hyperbolic tangent）

（8）指数运算符：ES2016 新增了一个指数运算符（**）
指数运算符可以与等号结合，形成一个新的赋值运算符（**=）；注意，在 V8 引擎中，指数运算符与Math.pow的实现不相同，对于特别大的运算结果，两者会有细微的差异，例：
Math.pow(99, 99)
// 3.697296376497263e+197
99 ** 99
// 3.697296376497268e+197


7、函数的扩展
（1）函数参数的默认值：ES6之前，不能直接给函数的参数指定默认值，只能采取变通的方法，例 function log(x, y ){ y= y || ' world'; console.log(x, y) }   同时此处还需要进行参数y是否被赋值，避免y赋值为“null”的情况，例 if( typeof y === undefined ) {y= 'world';} 
ES6允许为函数设置默认值，直接写在函数参数定义的后面；参数变量是默认声明的，不能用let 或者 const 再次声明；
参数默认值与解构赋值默认值结合使用：
参数默认值的位置：应该设置与尾部，若在中间，需显示输入undefined；
函数的length 属性：返回没有指定默认值的参数个数；
作用域：函数声明初始化时，参数会形成一个作用域；
（2）rest 参数（形式为 ...变量名）用于获取函数的多余参数，这样就不需要 arguments 对象了
rest 参数搭配的变量是一个数组，该变量将多余的参数放入数组中；
arguments 对象不是数组，而是一个类数组对象，使用数组的方法 Array.prototype.clice.call() 将其转换为数组；
【注意在rest 参数后面不得再有其他参数（即只能是最后是一个参数）】
（3）严格模式：' use strict'
ES6 规定只要韩素华参数使用了默认值、解构赋值、或者扩展运算符，那么函数内部不能显示设定为严格模式；
（4）name 属性：函数的name属性，返回该函数的函数名；
【注意：ES6中，若将一个匿名函数赋值给一个变量，name属性会返回实际的函数名，而ES5中的name属性，会返回空字符串；】
bind 返回的函数，name 属性会加上 bound 前缀；
（5）箭头函数：使用（"=>"）定义函数
箭头函数参数用小括号()包起来，函数体用大括号{}包起来；
使用注意点：函数体内的 this 对象，指向的是定义时所在的对象，而非使用时所在对象；
不可以当作构造函数，即不可以使用 new 命令；不可以使用 arguments 对象，该对象在函数体被不存在，可以使用 rest 参数代替；不可以使用  yield 命令，因此箭头函数不能用作  Generator 函数；【箭头函数中， this 对象的指向是固定的】
嵌套的箭头函数、部署管道机制（pipeline）两个范例程序；
（6）双冒号运算符：函数绑定运算符（ :: ），运算符左边是一个对象，右边是一个函数；该运算符会自动将左边的对象，作为上下文环境（即 this 对象），绑定到右边的函数上面；
例：foo :: bar;    等价于    bar.bind(foo);
foo :: bar(...arguments);    等价于    bar.apply(foo, arguments);   
(7)尾调用优化：
尾调用是函数式变成的一个重要概念，指的是某个函数的最后一步时调用另一个函数；
尾调用优化：只保留内层函数的调用帧；【注意只有不再调用到外层函数的内部变量，内层函数的调用帧才会取代外层函数的调用帧，否找无法进行“尾调用优化”】
尾递归：函数尾调用自身，尾递归只存在一个调用帧，不会存在“栈溢出”错误，其复杂度为O(1)；例 Fibonacci 数列的实现；
递归函数的改写：把所有用到的内部变量改成函数的参数；
柯里化：将多参数的函数转换为但参数的形式；
严格模式：
尾递归优化的是实现：
（8）函数参数尾逗号：新的语法允许定义和调用，尾部直接有一个逗号；


8、数组的扩展
（1）扩展运算符
含义：扩展运算符（spread）是三个点（...）；它好比 rest 参数的逆运算，将一个数组转为用逗号分隔的参数序列；该运算符主要用于函数调用

9、对象的扩展
（1）属性的简介表示法：ES6允许直接写入变量和函数，方法和属性都可以简写；
属性赋值器（setter）和取值器（getter）也可以这样写；
若某一个方法的值时一个Generator 函数，前面需要加上星号；
（2）属性名表达式：JavaScript定义对象的属性可以直接用标识符作为属性名，例obj.foo= true;   还可以用表达式作为属性名，即表达式放在方括号内，例 obj[ ' a '+ ' bc ']= 1123;
【注意，属性名表达式如果是一个对象，默认情况下会自动将对象转为字符串[object Object]，这一点要特别小心】
（3）方法的 name 属性：函数的name属性返回函数名。对象方法也是函数，因此也有name属性；如果对象的方法使用了取值函数（getter）和存值函数（setter），则name属性不是在该方法上面，而是该方法的属性的描述对象的get和set属性上面，返回值是方法名前加上get和set；
【注意：bind方法创造的函数，name属性返回bound加上原函数的名字；Function构造函数创造的函数，name属性返回anonymous】
（4）Object.is()：ES5 比较两个值是否相等，只有两个运算符：相等运算符（==）和严格相等运算符（===）。它们都有缺点，前者会自动转换数据类型，后者的NaN不等于自身，以及+0等于-0；
Object.is()方法是ES6 提出“Same-value equality”（同值相等）算法，用来比较两个值是否严格相等，与严格比较运算符（===）的行为基本一致；不同之处只有两个：一是+0不等于-0，二是NaN等于自身。
（5）Object.assign()方法：用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target）；该方法第一个参数是目标对象，后面的参数都是源对象；
【注意，如果目标对象与源对象有同名属性，或多个源对象有同名属性，则后面的属性会覆盖前面的属性；结果返回的是对象；因为undefined和null无法转成对象，所以它们无法作为参数；其他类型的值（即数值、字符串和布尔值）不在首参数，也不会报错。但是，除了字符串会以数组形式，拷贝入目标对象，其他值都不会产生效果，这是因为只有字符串的包装对象，会产生可枚举属性；Object.assign 拷贝的属性是有限制的，只拷贝源对象的自身属性（不拷贝继承属性），也不拷贝不可枚举的属性（enumerable: false）】
Object.assign()特点：
浅拷贝：如果源对象某个属性的值是对象，那么目标对象拷贝得到的是这个对象的引用；
同名属性的替换：一旦遇到同名属性，该方法处理方法是替换；而不是添加；
数组的处理：该方法可以用来处理数组，但是会把数组视为对象
取值函数的处理：该犯法只能进行值的复制，如果要复制的值是一个取值函数，那么将求值后再复制；
Object.assign()常见用途：
为对象添加属性；为对象添加方法；克隆对象；合并多个对象；为属性指定默认值；
（6）属性的可枚举性和遍历：
Object.getOwnPropertyDescriptor()方法可以获取该属性的描述对象( 该属性的行为)
可枚举性：描述对象的enumerable属性，目前有四个操作会忽略enumerable为false的属性。
* for...in循环：只遍历对象自身的和继承的可枚举的属性，toString和length属性的enumerable都是false，因此for...in不会遍历到这两个继承自原型的属性， ES6 规定，所有 Class 的原型的方法都是不可枚举的。（ES5）
* Object.keys()：返回对象自身的所有可枚举的属性的键名。（ES5）
* JSON.stringify()：只串行化对象自身的可枚举的属性。（ES5）
* Object.assign()： 忽略enumerable为false的属性，只拷贝对象自身的可枚举的属性。（ES6）
属性的遍历：ES6 一共有 5 种方法可以遍历对象的属性
1）for...in
for...in循环遍历对象自身的和继承的可枚举属性（不含 Symbol 属性）。
2）Object.keys(obj)
Object.keys返回一个数组，包括对象自身的（不含继承的）所有可枚举属性（不含 Symbol 属性）的键名。
3）Object.getOwnPropertyNames(obj)
Object.getOwnPropertyNames返回一个数组，包含对象自身的所有属性（不含 Symbol 属性，但是包括不可枚举属性）的键名。
4）Object.getOwnPropertySymbols(obj)
Object.getOwnPropertySymbols返回一个数组，包含对象自身的所有Symbol 属性的键名。
5）Reflect.ownKeys(obj)
Reflect.ownKeys返回一个数组，包含对象自身的所有键名，不管键名是Symbol 或字符串，也不管是否可枚举。
以上的 5 种方法遍历对象的键名，都遵守同样的属性遍历的次序规则:
* 首先遍历所有数值键，按照数值升序排列;
* 其次遍历所有字符串键，按照加入时间升序排列;
* 最后遍历所有 Symbol 键，按照加入时间升序排列;
(7)Object.getOwnPropertyDescriptors()方法：返回指定对象所有自身属性（非继承属性）的描述对象；而Object.getOwnPropertyDescriptor()方法会返回某个对象属性的描述对象（descriptor）;
该方法的引入目的，主要是为了解决Object.assign()无法正确拷贝get属性和set属性的问题；
Object.getOwnPropertyDescriptors()方法配合Object.defineProperties()方法，就可以实现正确拷贝它背后的赋值方法或取值方法；
Object.getOwnPropertyDescriptors()方法的另一个用处，是配合Object.create()方法，将对象属性克隆到一个新对象;

（8）__proto__属性，Object.setPrototypeOf()，Object.getPrototypeOf()
JavaScript 语言的对象继承是通过原型链实现的。ES6 提供了更多原型对象的操作方法；
__proto__属性（前后两个下划线）：用来读取或设置当前对象的prototype对象；它本质上是一个内部属性，而不是一个正式的对外的 API，只是由于浏览器广泛支持才被加入了 ES6；无论从语义的角度，还是从兼容性的角度，都不要使用这个属性，而是使用下面的Object.setPrototypeOf()（写操作）、Object.getPrototypeOf()（读操作）、Object.create()（生成操作）代替；
实现上，__proto__调用的是Object.prototype.__proto__；若一个对象本身部署了__proto__属性，该属性的值就是对象的原型；
Object.setPrototypeOf()方法：作用与__proto__相同，用来设置一个对象的prototype对象，返回参数对象本身。它是 ES6 正式推荐的设置原型对象的方法；格式    Object.setPrototypeOf(object, prototype);
Object.getPrototypeOf()方法：该方法与Object.setPrototypeOf()方法配套，用于读取一个对象的原型对象；
（9）super 关键字：指向当前对象的原型对象（ ES6）；而 this 关键字总是指向函数所在的当前对象；
【注意，super关键字表示原型对象时，只能用在对象的方法之中，用在其他地方都会报错；】
（10）Object.keys()，Object.values()，Object.entries()
Object.keys()返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键名；
Object.keys配套的Object.values和Object.entries，作为遍历一个对象的补充手段，供for...of循环使用。
Object.values()方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值;
Object.entries()方法返回一个数组，成员是参数对象自身的（不含继承的）所有可遍历（enumerable）属性的键值对数组;
（11）对象的扩展运算符（...）
解构赋值：对象的解构赋值用于从一个对象取值，相当于将目标对象自身的所有可遍历的（enumerable）、但尚未被读取的属性，分配到指定的对象上面。所有的键和它们的值，都会拷贝到新对象上面。
解构赋值要求等号右边是一个对象，所以如果等号右边是undefined或null，就会报错，因为它们无法转为对象；解构赋值是最后一个参数；
【注意，解构赋值的拷贝是浅拷贝，即如果一个键的值是复合类型的值（数组、对象、函数）、那么解构赋值拷贝的是这个值的引用，扩展运算符的解构赋值，不能复制继承自原型对象的属性】
完整克隆一个对象，还拷贝对象原型的属性，可以采用下面的写法：
// 写法一
const clone1 = {
__proto__: Object.getPrototypeOf(obj),
...obj
};
// 写法二
const clone2 = Object.assign(
Object.create(Object.getPrototypeOf(obj)),
obj
);
// 写法三
const clone3 = Object.create(
Object.getPrototypeOf(obj),
Object.getOwnPropertyDescriptors(obj))

写法一的__proto__属性在非浏览器的环境不一定部署，因此推荐使用写法二和写法三。


10、Symbol
（1）










11、Set和Map 数据结构
（1）












12、Proxy
（1）













13、Reflect
（1）













14、Promise 对象
（1）含义：简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，Promise 是一个对象，从它可以获取异步操作的消息。Promise 提供统一的 API，各种异步操作都可以用同样的方法进行处理；
Promise对象有以下两个特点：
对象的状态不受外界影响，Promise对象代表一个异步操作，有三种状态：pending（进行中）、fulfilled（已成功）和rejected（已失败）；
一旦状态改变，就不会再变，任何时候都可以得到这个结果；
Promise也有一些缺点：
首先，无法取消Promise，一旦新建它就会立即执行，无法中途取消。其次，如果不设置回调函数，Promise内部抛出的错误，不会反应到外部。第三，当处于pending状态时，无法得知目前进展到哪一个阶段（刚刚开始还是即将完成）；
（2）基本用法：ES6 规定，Promise对象是一个构造函数，用来生成Promise实例；Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject，例 const promise = new Promise(function(resolve, reject) {});
resolve函数的作用是，在异步操作成功时调用（从 pending 变为 resolved），并将异步操作的结果，作为参数传递出去；reject函数的作用是，，在异步操作失败时调用（从 pending 变为 rejected），并将异步操作报出的错误，作为参数传递出去;
Promise实例生成以后，可以用then()方法分别指定resolved状态和rejected状态的回调函数;then()方法可以接受两个回调函数作为参数。第一个回调函数是Promise对象的状态变为resolved时调用（必须的），第二个回调函数是Promise对象的状态变为rejected时调用。
（3）Promise.prototype.then()：then方法是定义在原型对象Promise.prototype上的，它的作用是为 Promise 实例添加状态改变时的回调函数；then方法的第一个参数是resolved状态的回调函数，第二个参数（可选）是rejected状态的回调函数；
（4）Promise.prototype.catch()：该方法是.then(null, rejection)的别名，用于指定发生错误时的回调函数；例：
getJSON('/posts.json').then(function(posts) {
  // ...
}).catch(function(error) {
  // 处理 getJSON 和 前一个回调函数运行时发生的错误
  console.log('发生错误！', error);});
上面代码中，getJSON方法返回一个 Promise 对象，如果该对象状态变为resolved，则会调用then方法指定的回调函数；如果异步操作抛出错误，状态就会变为rejected，就会调用catch方法指定的回调函数，处理这个错误。另外，then方法指定的回调函数，如果运行中抛出错误，也会被catch方法捕获。


【未看完】

15、lterator 和 for...of循环
（1）

16、Generator 函数的语法
（1）

17、Generator函数的异步应用
（1）

18、async 函数
（1）


19、 Class 的基本语法
（1）JavaScript 语言中，生成实例对象的传统方法是通过构造函数；
ES6 引入了 Class（类）这个概念，作为对象的模板。通过class关键字，可以定义类；
constructor表示构造方法，this关键字则代表实例对象，类的数据类型就是函数，类本身就指向构造函数。使用的时候，也是直接对类使用new命令，跟构造函数的用法完全一致，而类的所有方法都定义在类的prototype属性上面类的内部所有定义的方法，都是不可枚举的（non-enumerable）；
（2）类和模块的内部，默认就是严格模式，所以不需要使用use strict指定运行模式。只要你的代码写在类或模块之中，就只有严格模式可用。
（3）constructor方法：类的默认方法，通过new命令生成对象实例时，自动调用该方法。一个类必须有constructor方法，如果没有显式定义，一个空的constructor方法会被默认添加；该默认返回实例对象（即this），完全可以指定返回另外一个对象；
（4）类的实例对象：使用new命令生成类的实例对象；类的所有实例共享一个原型对象，所以实例对象它们的原型都是Point.prototype，所以__proto__属性是相等的；
（5）Class表达式：注意类名是表达式左边的名字，例 const MyClass = class Me {getClassName() {return Me.name;  }};//类的名字是MyClass而不是Me，Me只在 Class 的内部代码可用，指代当前类，也可以省略Me；
采用 Class 表达式，可以写出立即执行的 Class，例
let person = new class { 
        constructor(name) { this.name = name;  }
         sayName() { console.log(this.name);  }
    }('张三');
person.sayName(); // "张三"
（6）类不存在变量提升，与ES5完全不同；
（7）私有方法和私有属性的实现方法：
将私有方法移出模块，因为模块内部的所有方法都是对外可见的；
利用Symbol值的唯一性，将私有方法的名字命名为一个Symbol值；
私有属性的提案：
目前，有一个提案，为class加了私有属性。方法是在属性名之前，使用#表示；
（8）this 的指向：
类的方法内部如果含有this，它默认指向类的实例。但是，必须非常小心，一旦单独使用该方法，很可能报错；
解决方法：一个比较简单的解决方法是，在构造方法中绑定this，这样就不会找不到print方法了，例 class Logger {constructor() {
    this.printName = this.printName.bind(this);  }
  // ...}
另一种解决方法是使用箭头函数；还有一种解决方法是使用Proxy，获取方法的时候，自动绑定this；
（9）name 属性：返回紧跟在class关键字后面的类名；
（10）Class 的取值函数（getter）和存值函数（setter）：
在“类”的内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为；
（11）Class 的 Generator 方法：如果某个方法之前加上星号（*），就表示该方法是一个 Generator 函数；
（12）Class 的静态方法：在类的方法前加上static关键字，就表示该方法不会被实例继承，而是直接通过类来调用；静态方法可以与非静态方法重名；父类的静态方法，可以被子类继承；静态方法也是可以从super对象上调用的；
【注意，如果静态方法包含this关键字，这个this指的是类，而不是实例】
（13）Class 的静态属性和实例属性：
静态属性：指的是 Class 本身的属性，即Class.propName，而不是定义在实例对象（this）上的属性；
类的实例属性：可以用等式，写入类的定义之中；
类的静态属性：只要在上面的实例属性写法前面，加上static关键字就可以了
(14)new.target 属性:一般用在构造函数之中，返回new命令作用于的那个构造函数;【注意：子类继承父类时，new.target会返回子类】

20、Class 的继承
（1）简介：通过extends关键字实现继承；子类必须在constructor方法中调用super方法，否则新建实例时会报错。这是因为子类自己的this对象，必须先通过父类的构造函数完成塑造，得到与父类同样的实例属性和方法，然后再对其进行加工，加上子类自己的实例属性和方法。如果不调用super方法，子类就得不到this对象。
ES5 的继承，实质是先创造子类的实例对象this，然后再将父类的方法添加到this上面（Parent.apply(this)）。ES6 的继承机制完全不同，实质是先将父类实例对象的属性和方法，加到this上面（所以必须先调用super方法），然后再用子类的构造函数修改this；另一个需要注意的地方是，在子类的构造函数中，只有调用super之后，才可以使用this关键字，否则会报错，这是因为子类实例的构建，基于父类实例，只有super方法才能调用父类实例；最后，父类的静态方法，也会被子类继承；
（2）Object.getPrototypeOf()：可以用来从子类上获取父类；
（3）super 关键字，两种用法：
第一，super作为函数调用，代表父类的构造函数，ES6要求子类的构造函数必须执行一次 super 函数；【注意，super虽然代表了父类A的构造函数，但是返回的是子类B的实例，即super内部的this指的是B，因此super()在这里相当于A.prototype.constructor.call(this)】
第二，super作为对象时，在普通方法中，指向父类的原型对象；在静态方法中，指向父类；


【未看完】

21、 Decorator
（1）

22、Module 的语法
（1）

23、 Model的加载实现
（1）

24、编程风格
（1）

25、 读懂规则
（1）

26、ArrayBuffer
（1）

27、 最新提案
（1）