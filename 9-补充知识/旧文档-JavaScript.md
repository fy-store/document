# 关于本文档

> 本文档是作者本人总结的笔记
>
> 该笔记不适合新手，阅读该笔记需要具备一定的基础
>
> 请将该笔记作为查漏补缺或临时查阅的文档
>
> 该笔记和官方冲突部分请以官方为主
>
> 该笔记主要参考文档为 **[mdn](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript)** 
>
> 如果该笔记出现错误或者你对其中有疑问请联系作者
>
> 作者联系QQ： [946686638](http://wpa.qq.com/msgrd?v=3&uin=946686638&site=qq&menu=yes)



## JavaScript 简介

> js作者：Brendan Eich
>
> 由 Netscape（网景公司）的 Brendan Eich（布兰登·艾奇）于 1995年发布
>
> 前端组成部分：html css js 
>
> 结构(html) 样式(css) 行为(js) 相分离
>
> JavaScript 负责操作元素的行为
> 
> JavaScript 是一门动态的、弱类型的、解释性、脚本语言。
> 
> JavaScript 由三大部分组成： ECMAScript  DOM  BOM
> 
> ECMAScript 负责js的语法
> 
> DOM document object model 文档对象模型 用于操作html元素
> 
> BOM browser object model 浏览器对象模型 用于操作浏览器



## 变量声明

- es5 使用 var 作为声明变量的关键词

- 在后续的es6 中增加了 let 和 const

- var 声明变量的特点：

1. 变量提升

	- 使用 var 声明的变量会进行 变量提升

	- 在js的预解析过程中通篇扫描 将 var 声明的变量提升到逻辑的最顶端，值赋予 undefined 

2. 可重复声明

	- 重复声明的变量后面覆盖前面

3. 没有块级作用域

	- 在for循环等代码体中声明变量会被提升到全局，会造成变量泄漏而导致污染全局变量



## 数据类型

> 在js中数据类型分为原始值和引用值：

- 原始值 7 种：
	 | 数字   | 字符串 | 布尔    | 未定义    | 空   | 最大安全整数[es6] | 符号（唯一标识）[es6] |
	| ------ | ------ | ------- | --------- | ---- | ----------------- | --------------------- |
	| number | string | boolean | undefined | null | bigint            | symbol                |

- 引用值：
	- 只有一个 object 对象，以下都为衍生，即特殊的对象；
	- function 函数；array 数组；date 时间; json ...

> 在这些中数据类型外系统还提供了一些用于表示某种含义的关键字；

- NaN 非数；属于数字类型；在一些特殊情况下想要表达该数应该为数字但又没法用数字表达时出现；
- 例如：类型转换：
```js
var num = Number('a'); 
var num1 = 'a' ++; 
// 之类的
```

- Infinity 和 -Infinity 正无穷和负无穷，属于数字类型；超出最大/最小数字时出现；
- 或者 1/0 时出现，因为1中有无数个0，值溢出，使用 Infinity 表示；



## 原始值

- 原始值具有不可改变性：
```js
var num = 123; 
num = 456;
```
- 内存当中该空间的值是不可改变的，实际内部是舍弃原空间而更改到一个新的空间；
	
- 即：将存放 123 的这个空间舍弃而改变到这个新的存放有 456 的空间。

- 两者拷贝赋值区别：

- 原始值：
	- 赋值使用一个存放[原始值]的的变量时，将其内容拷贝(复制)一份赋予到新空间，
	- 与旧空间非同一个。

```js
var num = 10; 
var num1 = num;
// 将 num 空间中的值赋值一份出来存放到 num1 中去，num 和 num1 中存放的非同一个；
// 两者已经不是同一个了，num1 是一个全新的；即：
num = 20;
console.log(num1); // 10 做到你变我不变
```



## 引用值

- 引用值：
  - 赋值使用一个存放[引用值]的变量时，复制的仅是该空间的引用地址，
  - 两者指向的还是同一个空间。

```js
var arr = [1, 2];
var arr1 = arr;
// 仅将 arr 的引用地址复制一份放入 arr1 中，两者指向还是同一空间；
arr1.push(3);
console.log(arr); // [1, 2, 3] 指向同一空间，你变我也跟着改变
```



## 关于 typeof

- typeof 用于区分数据类型

- 使用方式有两种，括号包裹 或者 空格隔开

```js
// 示例：
typeof('hehe'); 
// 或者 
typeof 'hehe'; 
```

- typeof 识别出来返回结果数据类型字符串类型

- typeof 对于一个未经声明的变量使用不报错，返回 undefined，

- 但是若这块区域出现 let 或者 const 则会让其前面出现暂时性死区，这时使用typeof则会报错

```js
// 示例：
{
    typeof x;
    let x;
}
// 报错
```

- 可以区分除 null 外所有原始数据类型：
	| 数字   | 字符串 | 布尔    | 未定义    |   安全大整数[es6] | 符号（唯一标识）[es6] |
	| ------ | ------ | --------- | ---- | --------------- | --------------------- |
	| number | string | boolean | undefined | bigint          | symbol                |

- 而引用类型使用typeof 得到的都是 'object'

- typeof null 返回 'object'

- 关于 null ：null 空；历史遗留原因，用于给对象占位；
	
- 使用 Object.prototype.toString 方法可以区分 对象 数组 null，使用时改变 this 指向即可

```js
// 示例：
console.log(Object.prototype.toString.call({})); // [object Object]
console.log(Object.prototype.toString.call([])); // [object Array]
console.log(Object.prototype.toString.call(null)); // [object Null]
```

## 栈和堆

- 在js中，内存大致被划分为 **栈** 、**堆** 、**常量区**

- 原始值存放在栈结构中，栈结构类似一个有底没顶的箱子

- 先储存的将会放在底部，取值时先进去的永远在最后出来

- 堆结构则是一个散列的链表结构，引用值就存放在此处

- 在储存原始值时，值会直接放在栈内存中

- 引用值则存放在堆内存中，其引用地址则存放在栈内存



## 命名规范

> 命名规则
1. 命名必须以 英文字母 或者 _ 或者 $ 开头

2. 命名可以包括 英文字母 _ $ 数字

3. 命名不可以用系统的关键字、保留字作为变量名

- 多个单词组合以小驼峰命名法命名
- 示例：userName 首个单词的首字母小写后续单词首字母大写

- 构造函数、类命名使用大驼峰命名
- 示例：Person 每个组合单词的首字母都大写



## 书写位置

1. 行内js 局限性很大，只能针对事件进行添加，很少使用
```html
// 示例：
<a href ="javascript:alert('hehe');">点击</a>
```

2. 内嵌js 一般将其放在 body 的最下面

	- js是单线程会阻断后续代码，如果是要将其放在 head 内

	- 一般不用 windown.onload 事件，而是使用 document 绑定 DOMContentLoaded

	- 事件，在 DOM 加载完毕后执行js，而不会造成dom获取不到的情况

	- 需要注意的是 DOMContentLoaded 只能使用 addEventListener 方式绑定

```html
// 示例：
<script>
    document.addEventListener('DOMContentLoaded', function() {});
</script>
```

3. 外链js 引入外部js文件，需要注意的是引入外部js其 script 标签内不能书写代码

```html
// 示例：
<script src=""></script>
```



## 书写规范

> js语句基本规则：

- 语句后面要用分号 ; 结束 像 {} 等后面则不需要

- js语法错误会引发后续代码终止，但不会影响其他的js代码块

- 各个script元素内js出错不会互相影响，还可跨越代码块使用值

- 书写格式规范，= + * / 两边都应该有一个空格

> 错误分两种：
- 低级错误（语法解析错误）

- 逻辑错误（标准错误）



## 算数运算符

> 运算操作符（算数运算符）：
```html
+ - * / %
```

>  \+ 特殊点

- 当两边有一个为字符串则调用 String 做字符串连接处理

```html
// 示例：
10 + '24' ==> '1024'
```

- 第二种情况
```html
// 示例：
true + true ==> 2

{} + 1 ==> '[object Object]1' 

[] + 1 ==> '1'
```



## 优先级

- = 最弱 () 优先级较高

- ++ -- 优先级大于 * /

- ++ 自增

- -- 自减

```js
var a = 1; 
a = a++;
// 结果为 1
```



> ++、-- 先后问题：

1. 先++

- 取常量区1 先在原空间++ 然后产生临时空间 再将临时空间的值赋出去

2. 后++

- 先产生临时空间 然后取常量区1 在原空间++ 而后再将临时空间的值赋出去



## 赋值运算符

赋值运算符：

```html
= += -= *= /= %=
```

- 赋值的顺序 自右向左

- 计算的顺序 自左向右

> 注意点：

- var a = 1 / 0; 打印 Infinity 表示 无穷

- var a = - 1 / 0; 打印 -Infinity 表示 负无穷

- 注意：Infinity 是数字类型

- var a = 0 / 0; 打印 NAN 表示 非数

- 凡是应该得出数值类型的值，但无法表示

- 则会换成 NAN 表示 非数

- 注意：NAN 是数字类型 



## 比较运算符

> 比较运算符（关系运算符）：

```txt
>  <  ==  >=  <=  !=
```

+ 比较的结果为boolean值

+ var a = NaN == NaN; // 返回 false

+ NaN (非数)在任何情况下都不等于任何数包括它自身 



## 逻辑运算符

> 运算符：

- &&（与，并且）|| （或，或者）!（非，取反）

> 定为 false 的值

- defind null NaN ""(空串) 0 false

- 除这6个值以外其余均为 true

> &&

```js
var a = 1 && 2 && 3;
```

- 第一个表达式，将其转换为布尔值，为 true

- 继续看第二个表达式，将其转换为布尔值，为 true

- 则继续...直到遇到 false 即停止并将该表达式返回

- 若其是最后一个表达式，则不看其布尔值且直接返回表达式

> 总结：遇 false 即停，并将其表达式返回

> 可用于短路语句：
```js
2 > 1 && document.write("hehe");
var date = ...;
date && document.write("hehe");
// 当后端传数据过来时，我们不确定是否有数据即可用短路语句判断
```

> ||

```js
var b = undefind || "" || 1 || null;
```

- 先看第一个表达式，将其转换为布尔值，为 false

- 则继续看第二个表达式，将其转换为布尔值，为 false

- 则继续...直到遇到 true 即停止并将该表达式返回

- 若其是最后一个表达式，则不看其布尔值且直接返回表达式

> 总结：遇 true 即停，并将其表达式返回 可用于兼容


> !

```js
var c = ! 123;
```

- 转为布尔值取反，true 变 false

- var d = !! 123; 取反后再取反 布尔值为 true

## 三目运算符

> 条件判断 ？是 ：否 并且会返回值

```js
let test = 1 > 0 ? 2 + 2 : 1 + 1;
// 返回：4
```

## 显示类型转换

- Number(value)

	- 将值转为数字类型 失败则返回数字类型 NAN

	- 注意：null 返回 0；true 返回 1；false 返回 0；
- String(value)

	- 将参数内的值转化为字符串类型
	- 数组转为字符串变成以逗号分割的数据 String([1,2,3]) ==> '1,2,3'
	- 转换对象都将返回 '[object Object]' 对象转换应当调用 json 方法
- Boolean(value)

	- 转为布尔值 除 undefined null NaN ''(空串) 0 false 这六个值以外，其余结果都为 true

## 隐式类型转换

> 隐式类型转换内部调用的都是显示类型

- ++ --  + - (一元正负) 调用 Number()

- \+ 当两边有一个为字符串则调用 String 做字符串连接处理

> \+ 的原理：

```txt
                            |--> 有字符串都转为字符串 --> 字符串拼接
           |--> 均为原始值-->|
           |                |--> 无字符串都转为数字 --> 加法（两端有一个为 NaN 得 NaN）
加法运算--> |
           |
           |--> 含有对象类型 --> 调用 valueOf（看能否转为原始值）
                                           ↓
                               调用 toString（看能否转为原始值）
                                           ↓
                                          报错
```

> 注意点：

- 1 + {} 返回 '1[object Object]'

- {} + 1 返回 1

- 出现这种差异是因为js解析将第二个 {} 当成一个代码块而非表达式

- => {code...}    +1 后面的则看做表达式一元正负的 +1

- 解决只需要加上括号就会把它作为表达式 ({} + 1) 返回 '[object Object]1'


> \- * / %

- 调用 Number()


> && || !

- 调用 Boolean()


> <  >  <=   >=

- 有数字则调用 Number() // 1 < '2'

- 字符串和字符串比较则比较 asc 码 // '10' > '2' 

- 首位比较：

```js
'9' > '8' // 返回 true

'19' > '8' // 返回 false

// 首位相等 再看后位 直到最后一位 若首位大于则不看后续

'23' > '2' // 返回 true

'234' > '234' // 返回 false

'bac' > 'bab' // 返回 true


1 > 'a' 

// 此种情况也比较 asc码 数字与字符串比较可以转换则比较数字 其余都是比较 asc码
// 比较后的最终返回结果是布尔值 true 或 false
```

> == !=

- 有数字则调用 Number() // 1 == '2'

> 无隐式调用情况：

- 原始值比对值

- 引用值比对地址

- 例子1：

```js
{} == {}

// 返回 false

// 虽然形式上一样但它是两个空间

// 引用的空间地址不一样
```

- 例子2：

```js
var a = [1,2];

var b = "1,2";

var c = a == b;

console.log(c); // true

// 这种情况则数组 调用 String() 方法

// 比较后的最终返回结果是布尔值 true 或 false
```

## == 规则

```txt
                |--> undefined == null
    |--> 特殊 -->|
    |           |--> NaN != NaN 
    |
==  |--> 类型相同 --> 比较值
    |
    |              |--> 均为原始值 --> 转为数字比较
    |--> 类型不同 -->|
                   |--> 一端原始值,一端对象 --> 对象转原始值后比较
                                                      ↓
                                              先调用 valueOf
                                                      ↓
                                              若无法转换成原始值，
                                              再调用 toString
```

## 特殊点

```js
// undefined 
undefined > 0
// 返回 false
undefined < 0
// 返回 false
undefined == 0
// 返回 false

// null 
null > 0
// 返回 false
null < 0
// 返回 false
null == 0
// 返回 false

// 那么 
undefined == null
// 返回 true
```

## 不发生类型转换

- === 绝对等于

- !== 绝对不等于

> 注意：

- NaN == NaN // 返回 false

- NaN === NaN // 返回 false

- NaN 不等于任何数 包括自身（任何情况下 NaN 都不等于 NaN）

## if 条件判断语句

```txt
if(条件) {
    // 执行语句
}
// 条件转为布尔值 为 true 则执行语句

if() {

}else{
  // 除了以外，其上的补集
}

if(条件) {

}else if(条件) {
  // 除了以外再判断
}
```

## switch 条件匹配语句

```js
// switch case 条件匹配语句

  switch(2) {
    case 1:
      console.log("a");
      break;
    case 2:
      console.log("b");
      break;
    case 3:
      console.log("c");
      break;
    default:
      console.log('所有都不匹配时输出');
      break;
  }
```

> swich 语句

- 若case判断第一个成功，尽管不在判断后面的 case 语句

- 但其依然会执行后面 case 里的内容（下漏，机械执行）

- 所以为了消除这种效果会在 case 语句最后加上 break 进行终止

- break 终止语句 终止循环（跳出循环）

- break 只能放在 switch 和循环里，否则会报错

> default

- default 所有的 case 都不匹配时执行 一般放在最后

> continue

- 终止本次循环，进行下一次循环 使用方法同 break

> switch case 

- 使用严格比较（===）值必须与要匹配的类型相同。

## for 循环

1. 第一步：声明变量 i 赋值为 0；

2. 第二步：判断 i 是否小于 10；

3. 第三步：执行代码体；

4. 第四步：i ++；

5. 第五步：判断 i 是否小于 10；

6. 第六步：i ++；

```js
// 示例：
for(let i = 0; i < 10; i++) {
    // code...
}
```

> 变形（类型while循环）：

- 变量声明放在语句外，变化值放在执行体

```js
// 示例：
let i = 0;
for(; i < 10;) {
    // code...
    i++;
}
```

## while 循环

- 条件转为布尔值，为 true 则执行

- 第一步：判断条件；

- 第二步：执行语句；

```js
// 示例：
let i = 0;
while(i < 10) {
    console.log(i);
    i ++;
}
// 输出 0 1 2 3 4 5 6 7 8 9
```

## do while 循环

- 仅作了解，开发不用

- 先执行一遍语句，然后再判断条件

```js
// 示例：
let i = 0;
do {
    console.log(i);
    i++;
} while (i < 10);
```

## function 函数

> 以关键字 function 定义函数(方法)

> 函数是具有作用域的，函数为局部作用域

> 函数声明：

```js
function test() {}
```

> 匿名函数：

```js
function () {}
```

> 命名函数表达式：

- 会忽略函数的命名，所以该表达式只能找到 fun

```js
let fun = function test () {}
```

> 匿名函数表达式：

- 因为会忽略函数的命名，索性就去掉；

- 所以一般而言 函数表达式 指的就是 匿名函数表达式

```js
let fun = function () {}
```

## 函数的特点

> 函数的特点：

```js
let fun = function (形参) {
    arguments // 实参列表 类数组
}
fun(实参);

// 当形参定义时内部会隐式定义变量
let fun = function(a, b, c) {
    // 隐式声明
    // var a, var b, var c;
}
```

## 立即执行函数

> 立即执行函数同样忽略函数命名；

> 此类函数没有声明，在一次执行过后即立即释放，适合做初始化工作；

>立即执行函数的两种写法：

```js
// 官方推荐
(function () {}()); 
// 第二种写法：
(function () {})();
```

> 实际上只要是表达式就能被执行符号执行 [执行符号 ()]

> 表达式：

```js
123;
123 + 234;
'test';
'test' + 'hehe';
```

> 测试

```js
  function demo () {
    console.log('aaa');
  }(); // 这样报错
```

> 这样书写不报错，但是不执行函数；

```js
function demo () {
  console.log('aaa');
}(1,2,3); // 这样不报错

// js会把它当做以下处理：
function demo () {
  console.log('aaa');
} 
// .
// .
// .
(1,2,3); // 会把它当成表达式
```

> 而这样就把它变成表达式，则可正常执行

```js
+ function demo() {
	console.log('aaa');
}(); // 正常执行 该处的 + 为一元正负的 +
```

## 预编译

> js运行三步：

1. 语法分析

2. 预编译

3. 解释执行

> 预编译前奏

- imply global 暗示全局变量：

- 即任何变量，如果变量未经声明就赋值，不报错，此变量就为全局对象所有。

- 例如：ege = 2; 未经声明即赋值，归全局所有 

- 全局即 window 一切未经声明的全局变量也是 window 的属性。

- 例如：var a = 123; => window.a = 123;

- a = 10; => window.a = 10; window 就是全局变量的域。

## AO 对象

> 函数预编译：

- 函数执行前一刻：

1. 创建 AO 对象 Activation Object （执行期上下文）

2. 找形参和变量声明，将变量和形参名作为AO对象的属性名，值为 undefined

3. 将实参和形参统一

4. 在函数体里面找函数声明，值赋予函数体

## GO 对象

> 全局预编译：

1. 生成一个 GO 对象 Global Object GO === window

2. 找变量声明，将变量作为 GO 对象的属性名，值为 undefined

3. 在函数体里面找函数声明，值赋予函数体

## 作用域

> 作用域定义：

- 变量（变量作用于又称上下文）和函数生效（能被访问）的区域

- [[scope]]:每个 javascript 函数都是一个对象，对象中有些属性我们可以访问，但有些不可以，

- 这些属性仅供 javascript 引擎存取，[[scope]] 就是其中一个

- [[scope]] 指的就是我们所说的作用域，其中存储了执行期上下文的集合

- 即：[[scope]] {执行期上下文}

## 作用域链

> 作用域链：

- [[scope]] 中所存储的执行期上下文对象的集合，这个集合呈链式链接，

- 我们把这种链式链接叫做作用域链。

> 执行期上下文：

- 当函数执行时，会创建一个称为 执行期上下文的内部对象。

- 一个执行期上下文定义了一个函数执行时的环境，

- 函数每次执行时对应的执行期上下文都是独一无二的，

- 所以多次调用一个函数会导致创建多个执行期上下文，

- 当函数执行完毕，它所产生的执行期上下文被销毁。

> 查找变量：

- 从作用域的顶端依次向下查找。

```js
// 示例：
let x = 10;
let fun = function () {
    let x = 20;
}
fun();

// 当其运行时的作用域为：
[[scope]] {
    fun : {
        x: 20
    },
    window : {
        x: 10
        // ...
    }
}
```

- 执行期上下文 ==> 函数执行时的一个环境

- 一个个执行期上下文通过链式链接 ==> 作用域链

- [[scope]] ==> 这个对象存放作用域链

- [[scope]] 被称为作用域

- 函数在执行后首先拿到的是全局的执行期上下文[0]

- 随后在拿到外层的执行期上下文，这时会将之前的往下挤

- 最后拿到自己的执行期上下文，示例如下：

```txt
[[scope]] {
    自己的: {},     // 0
    外层函数的: {}, // 1
    外层函数的: {}, // 2
    外层函数的: {}, // 3
    // ...        // ...
    全局的: {}     // 全局的被挤到最下
}

当取值查找时，自顶向下查找，先查找自己的
如果没有则找外层的，最后查找全局
```

## 闭包

> 定义：

- 当内部函数被保存到外部时，将会生成闭包。

- 闭包会导致原有作用域链不释放，造成内存泄漏。

> 闭包的作用：

- 实现公有变量（例如：函数累加器）

- 可以做缓存（储存结构）

- 可以实现封装，属性私有化

- 模块化开发，防止污染全局变量


> 闭包示例：

```js
let a = 10;
let fun = function () {
    let a = 20;
    return function () {
        a++;
        console.log(a);
    }
}
let newFun = fun();
```

- 此刻 fun return 出来了一个函数，

- 随后这个函数被外部的一个变量 newFun 保存，

- 这时 newFun 拿到了 返回函数 的引用，

- 因为这条引用，返回函数具有 fun 的 执行期上下文，

- fun 没有砍断所有联系 所以不能被销毁 此时的场景便形成了闭包。

- 每当 newFun 执行一次时就会顺着作用域链查找而使用到 fun 的变量。

```js
newFun(); // 21
newFun(); // 22
newFun(); // 23
```

- 此刻 fun 函数的变量 a 就变成了私有变量

- 过多的闭包会占用太多的资源，所以在开发中需要注意

## Array 数组

> 数组是一种类列表对象，它的原型中提供了遍历和修改元素的相关操作。

> JavaScript 数组的长度和元素类型都是非固定的。

> 因为数组的长度可随时改变，并且其数据在内存中也可以不连续，

> 所以 JavaScript 数组不一定是密集型的，这取决于它的使用方式。。

## 创建数组

> 数组字面量：

```js
  let arr = []; --> new Array();
```

> 系统自带构造函数：

```js
let arr = new Array(正常添值);
```

> 数组的方法来自：Array.prototype

> 字面量和构造函数的唯一区别：

```js
let arr = Array(6);
// 添一位时表示数组的长度，会让其内容为 空 撑开
```

## Array 对象

> Array 的常用属性和方法

> Array.length 
>
> 查看数组长度

- 语法：**arr.length**

```js
let arr = [1, 2, 3];
arr.length;
```

> Array.prototype.concat() 
>
> 用于合并两个或多个数组；不改变原数组，返回新数组；

- 语法：**var new_array = old_array.concat(value1 [, value2 [, ...[, valueN]]])**

- 注意：拼接后的数组的引用类型的值是进行浅拷贝（仅复制引用地址）

```js
let arr = [1,2,3];
let arr2 = [4,5,6];
let arr3 = [7,8,9];
let newArr = arr.concat(arr2,arr3);
```

> Array.prototype.filter() 
>
> 创建一个新数组，其包含通过所提供函数实现的测试的所有元素

 - 语法：**var newArray = arr.filter(callback(elm [, index [, arr]]) [, thisArg])**

   - callback：回调函数

   - elm：当前正在处理的元素

   - index：正在处理的元素在数组中的索引[可选]

   - arr：调用了 filter 的数组本身[可选]

   - thisArg：执行 callback 时，内部this指向[可选]

 - 注意：创建新数组，不改变原数组；返回 true 才会将其放入新数组；

   - filter 遍历的元素范围在第一次调用 callback 之前就已经确定了
   - 在调用 filter 之后被添加到数组中的元素不会被 filter 遍历到
   - 如果已经存在的元素被改变了，则他们传入 callback 的值是 filter 遍历到它们那一刻的值
   - 被删除或从来未被赋值的元素（空）不会被遍历到

```js
let arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 17];
let newArr = arr.filter(function (elm, index, arr) {
    if(elm > 10) return true;
});    
```

> Array.prototype.find() 
>
> 返回数组中满足提供的测试函数的第一个元素的值；匹配失败返回 undefined

- 语法：**arr.find((callback(elm [, index [, arr]]) [, thisArg])**
  - callback：回调函数
  - elm：当前正在处理的元素
  - index：正在处理的元素在数组中的索引[可选]
  - arr：调用了 filter 的数组本身[可选]
  - thisArg：执行 callback 时，内部this指向[可选]
- 注意：true 则返回；
  - 只匹配第一次符合的项，后续不再继续遍历；
  - 数组中的空项同样遍历；
  - 不改变原数组；

```js
let arr = [1,2,3,4,5,6,7,8,9,10];
console.log(arr.find((elm, index, arr)=> {
    if(elm % 2 == 0) {
        return true;
    }
})); // 2
```

> Array.prototype.forEach() [es6]
>
> 对数组的每个元素执行一次给定的函数（遍历）

- 语法：**arr.forEach(elm [, index [, arr]]) [, thisArg])**
- 注意：forEach() 是对数组的每一项都进行处理
  - 但是不对空项进行处理（空项不调用函数）

```js
let arr = [1,2,3,4,,,7,8,9,10];
console.log(arr.forEach((elm, index, arr)=> {
    if(elm % 2 == 0) {
        console.log(elm);
    }
})); // 2 4 8 10
```

> Array.prototype.includes()
>
> 对该数组查找某个值

- 语法：**arr.includes(valueToFind [, fromIndex])**
  - valueToFind需要查找的值；
  - fromIndex指定从哪开始查找的索引位，可为负（倒数）；
- 注意：会对数组的每一项进行匹配；返回结果为布尔值 true / false

```js
let arr = ['a','b','c'];
console.log(arr.includes('a')); // true
```

> Array.prototype.indexOf() 
>
> 返回在数组中可以找到一个给定元素的第一个索引，如果不存在，则返回-1

-  语法：**arr.indexOf(searchElement [, fromIndex])**
  - searchElement需要查找的值；
  - fromIndex指定开始查找的索引为，可为负倒数）；
- 注意：返回的值为匹配成功项的索引位 失败则返回 -1

```js
let arr = ['a','b','c'];
console.log(arr.indexOf('b')); // 1
```

> Array.isArray() 
>
> 用于确定传递的值是否是一个 Array

- 语法：**Array.isArray(obj) **
  - obj需要检测的值
- 注意：返回一个布尔值

```js
console.log(Array.isArray({})); // false
console.log(Array.isArray([])); // true
console.log(Array.isArray(null)); // false
```

> Array.prototype.join() 
>
> 将一个数组（或一个类数组对象）的所有元素以特定方式连接成一个字符串

- 语法：**arr.join(str])**
-  注意：以特定方式将数组连接成一个字符串；
  - 不改变原数组，返回值是连接后的字符串；
  - 传入参数为连接方式，不传参默认以 , 逗号连接；

```js
let arr = [1, 2, 3, 4, 5];
let newArr = arr.join('-');
console.log(newArr); // 1-2-3-4-5
```

> Array.prototype.lastIndexOf() 
>
> 匹配一个值 从后面往前查找；

- 语法：**arr.lastIndexOf(searchElement[, fromIndex]) **
  - searchElement需要查找的值；
  - fromIndex指定开始查找的索引为，可为负；
- 注意：其从后面往前查询，匹配第一个符合值，返回其索引位；查找失败返回 -1；

```js
let arr = ['a','b','c','a'];
console.log(arr.lastIndexOf('a')); // 3
```

> Array.prototype.map() [es6] 
>
> 创建一个新数组，这个新数组由原数组中的每个元素都调用一次提供的函数后的返回值组成

- 语法：**let new_array = arr.map(callback(elm [, index [, arr]]) [, thisArg])**
- 注意：对每一项调用函数，执行其返回值；
  - 但对于空白项不会遍历到，会直接跳过此项；
  - 所以若含未赋值的空白项，打印index不会拥有；
  - 创建一个新数组，存的是返回值结果

```js
let arr = [1,2,3,4,5,6,7,,9,10];
let newArr = arr.map((elm, index, array)=> {
    console.log(index) // 0 1 2 3 4 5 6 8 9 空白项跳过不会有 7
    return elm + 1;
});
console.log(newArr); // [2, 3, 4, 5, 6, 7, 8, 空白, 10, 11]
```

> Array.prototype.pop() 
>
> 删除数组最后一个元素,改变原数组;

- 语法：**arr.pop()**
- 注意：该删除实际为剪切
  - 剪切数组中最后一个元素，并将剪切的值返回；
  - 该方法改变原数组；
  - 空数组调用将返回 undefined

```js
let arr = [1, 2, 3, 4, 5];
let newArr = arr.pop();
console.log(arr); // [1, 2, 3, 4]
console.log(newArr); // 5
```

> Array.prototype.push() 
>
> 在数组最后增加元素（可同时增加多个）

- 语法：**arr.push(element1, ..., elementN)**
- 注意：该方法改变原数组，该方法的返回值为新的 length

```js
let arr = [1, 2, 3, 4, 5];
arr.push(6,7);
console.log(arr); // [1, 2, 3, 4, 5, 6, 7]
```

> Array.prototype.reverse() 
>
> 逆反数组排列顺序

- 语法：**arr.reverse()**
- 注意：该方法会改变原数组，其返回值也是改变后的数组（是同一个）

```js
let arr = [1, 2, 3, 4, 5];
let newArr = arr.reverse();
console.log(arr); // [5, 4, 3, 2, 1]
console.log(newArr); // [5, 4, 3, 2, 1]
// arr === newArr 返回 true
```

> Array.prototype.shift() 
>
> 删除数组第一个元素，改变原数组；

- 语法：**arr.shift()**
- 注意：删除数组第一个值（剪切）
  - 改变原数组，返回值为剪切出来的值
  - 空数组调用则返回 undefined

```js
let arr = [1, 2, 3, 4, 5];
let newArr = arr.shift();
console.log(arr); // [2, 3, 4, 5]
console.log(newArr); // 1
```

> Array.prototype.slice() 
>
> 剪切数组中的某项元素

- 语法：**arr.slice([begin[, end]])**
  -  begin起始位置；
  - end结束位置；
  - 参数可为负数（倒数）；
- 注意：截取数组中的某项元素，还是以数组形式返回截取的元素，不改变原数组；
  - 不传参数（空截）则截取一整个，截取出来的是一个新数组，绝对不等于原数组；
  - 传入一个参数则以该索引为起始位，截取到最后；
  - 截取只能为顺序截取，例如：2,3 [2到3]; 不能逆序截取，例如：3,2 [3到2]
  - 不改变原数组，并且其剪切出来的是一个浅拷贝的值；

```js
let arr = [1, 2, 3, 4, 5];
let newArr = arr.slice(2,3);
console.log(newArr); // [3]
```

> Array.prototype.sort() 
>
> 对数组排序

- 语法：**arr.sort([compareFunction])**
- 注意：不传参默认排序方式以asc码表排；传入参数则按返回值排序；
  - 回调参数规则：
  - 必须写两个形参
  - 看返回值：
  - 当返回值为负数时，那么前面的数放在前面
  - 当返回值为正数时，那么后面的数在前
  - 当返回值为 0 时，那么不进行变动
  - 升序 return a - b;
  -  降序：return b - a;
  -  乱序：return Math.random() - 0.5;
  - 该方法改变原数组，并且返回值是改变后的数组

```js
let arr = [1,3,-2,-5,5,5,10,8,4];
let num = arr.sort(function (a, b) {
  // 升序
  // if (a > b) {
  //     return 1;
  // }else {
  //     return -1;
  // }

  // 简化升序
  return a - b;

  // 降序
  // if (a < b) {
  //     return 1;
  // }else {
  //     return -1;
  // }

  // 简化降序
  // return -(a - b);
  // 再简化
  // return b - a;

    // 乱序
  // return Math.random() - 0.5;
});
// 该函数会被调用多次
// 第一次执行时会把数组第一位和第二位放进去
// 第二次执行时会把数组第一位和第三位放进去
// 第三次执行时会把数组第一位和第四位放进去
```

> Array.prototype.splice() 
>
> 截取添加（剪切替换）

- ​    语法：**arr.splice(index [,len] [,newElm]);** 
  - index截取的起始索引位；
  - len截取长度（截取多长/截取几个）；
  - newElm切口处新增的元素；
- 注意：不传参则不截取；
  - 一个参数则从第几位开始截取 截取到最后；
  - 两个参数 从第几位开始截取 截取多长/截取几个；
  - 第三个参数 在截取的切口出添加新的数据
  - 该方法改变原数组，其返回值为截取出来的数据，以数组形式存在；

```js
let arr = [1,2,3,4,5,6];
let newArr = arr.splice(2, 1, 0, 0, 0);
console.log(arr); // [1, 2, 0, 0, 0, 4, 5, 6]
console.log(newArr); // [3]
```

> Array.prototype.toString() 
>
> 将数组以逗号分割转为字符串

- 语法：**arr.toString()**
- 注意：该方法不改变原数组，返回新数组；
  - Array对象覆盖了 Object.prototype 上的 toString 方法；

```js
let arr = [1,2,3,4,5,6];
let newArr = arr.toString();
console.log(newArr); // 1,2,3,4,5,6
```

> Array.prototype.unshift() 
>
> 将一个或多个元素添加到数组的开头，该方法修改原有数组

- 语法：**arr.unshift(element1, ..., elementN)**
- 注意：在数组开头增加新数据，改变原数组；
  - 返回值为改变后新数组的长度；

```js
let arr = [1,2,3,4,5,6];
arr.unshift(0,0,0);
console.log(arr); // [0, 0, 0, 1, 2, 3, 4, 5, 6]
```

> 文档地址：
https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array

## Object 对象

>  对象的创建方法：

- 字面量：

```js
let obj = {} // 底层 new Object()
obj.userName = 'hehe';
obj.userAge = 19;
```

- 系统构造函数：

```js
let obj = new Object();
obj.userName = 'hehe';
obj.userAge = 19;
// 注意 构造函数通过 new 产生对象
```

- 自定义构造函数：

```js
let TestFun = function (x, xx) {
    this.x = x;
    this.xx = xx;
}

let test = new TestFun('test1','test2');
test.userName = 'hehe';
test.userAge = 19;
// 注意 构造函数通过 new 产生对象
```

- 垃圾回收机制

```js
// 垃圾回收 GC
// 当一个空间没有再被引用时会被销毁
// 对象取消引用：
let obj = {}
obj = null;
```

## 构造函数

- 构造函数一般都是以大驼峰命名
- 系统提供的构造函数：Object(); Array(); Number(); Boolean(); String(); Date(); ...
- 构造函数本身是一个函数，通过使用 new 可以构建出对象，相当于对象的生产工厂

```js
// 自定义：构造函数
function Person (age) {
	// var this = {name: 'lai', age: age}
	// 即 AO {this: {name: 'lai'}}
	this.name = 'lai';
	this.age = age;
	// return this;
	// 修改隐式 return 的值返回一个对象/数组将会覆盖系统的返回值 其它则无效
}
let person1 = new Person(17);
let person2 = new Person(18);

// 构造函数内部原理：
// 1. 在函数体最前面隐式的加上 this = {}
// 2. 执行 this.xxx = xxx;
// 3.隐式的返回this
```

## 包装类

1. new String()

2. new Boolean()

3. new Number()

> 例子1：

```js
var str = new String('aaa');
str.a = 'eee';
// 访问 str.a undefined
```

> 例子2：

```js
  var num = 4;
  num.len = 3;
  // new Number(4).len = 3;  --> delete
  console.log(num.len); // new Number(4).len
  // 最终返回 undefined
```

> 注意：字符串可以调用 length 属性，因为字符串底层是基于数组的，其原型上有这个属性。

## 原型

> 原型是function 对象的一个属性，它定义了构造函数制造出来的对象的公共祖先。

> 通过该构造函数产生的对象，可以继承该原型的属性和方法。原型也是对象。

> 利用原型的特点和概念，可以提取公有属性。

> 对象如何查看原型 => 隐式属性  \__proto__

> 对象如何查看对象的构造函数 => 属性 constructor

> 原型：prototype

```js
let Person = function (name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Person.prototype = {
    from: 'china'
}

let person1 = new Person('hehe', 19, 'man');
let person2 = new Person('haha', 20, 'woman');
```
- 控制台 person.constructor 即可查看构造它的函数是谁
- 控制台 person.\__proto__ 即可查看构造它的原型
- 命名方法：_abc _开头的 即告诉他人尽量别动它


> 修改 \__proto__

- \__proto__ 作为原型指向的隐式属性
- 修改 \__proto__ 即可修改原型指向

```js
let Person = function (name, age, sex) {
    // var this = {
    // __proto__:Person.prototype
	// }
    this.name = name;
    this.age = age;
    this.sex = sex;
    this.__proto__ = obj; 
    // __proto__ 作为原型指向的隐式属性
    // 修改 __proto__ 即可修改原型指向
}
Person.prototype = {
    from: 'china'
}
let obj = {
    from: '大唐'
}

let person1 = new Person('hehe', 19, 'man');
let person2 = new Person('haha', 20, 'woman');

// 此刻访问 person1.from
// 返回 ‘大唐’
```

> 增删改查同对象一致

```js
// 例子：
Person.prototype.name = 'sunny';
function Person() {
// var this = {__proto__ : Person.prototype} Person.prototype 指向的是一个对象空间
}
var person = new Person(); 
// 执行后 保存 var this = {__proto__ : Person.prototype} Person.prototype 指向的那个对象空间 这里存的是引用

Person.prototype = {
name: 'cherry'
}
// 改变 Person.prototype 指向的那个空间引用 但 person 里的可没改变 变得是 Person
// 访问  person.name 返回 sunny ； 访问  Person.name 返回 cherry 
// 可参考下方
var obj = {
name : 'a'
}
var obj1 = obj;
obj = {
name : 'b'
}
```

## 关于 \__proto__

- 对象查找原型是通过隐式属性 \__proto__

```js
let Person = function() {
    this.__proto__ = {}
}
Person.prototype.name = 'hehe';
let person = new Person();
// 访问 person.name 返回 undefined
// 因为 this.__proto__ = {} 将原型指向修改到一个新的空对象
// 而 Person.prototype 指向的还是旧的那个对象
// 此时 访问 Person.prototype 就可以找到旧的那个对象
```



## 关于 constructor

```js
// constructor 是对象上的一个属性
let arr = [];
arr.constructor === Array;
// true
// 用来判断实例该对象的构造函数
// 可以用来判断数据类型 Object.prototype.toString 同样可以判断数据类型
```

## 原型链

- 多个对象通过其原型或修改原型指向达成联系
- 通过链式串联在一起达到继承效果即为原型链

```js
let Father = function(money, car) {
    this.money = money;
    this.car = car;
}
Father.prototype = {
    house: '大房子'
}
let Me = function(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Me.prototype = new Father('many', '四轮'); // new Father 后返回一个对象，Me原型指向该对象
let me = new Me('hehe', 19, 'man');
```

> 原型链上属性的增删改查

- 增删改只能自身修改 后代无法修改父级

> Object.create(原型);

- 一种更加灵活的构造对象方法 可以自己指定原型

```js
let obj = {
    name: 'hehe',
    age: 19,
    sex: 'man'
}
let newObj = Object.create(obj);
// 访问 newObj.name 返回 ‘hehe'
```

> 绝大多数 对象 的最终都会继承自 Object.prototype

```javascript
// 例外：
let obj = Object.create(null); 
// 填 null 没有原型 但它生产出的仍然是一个对象
// obj.__proto__ 返回 undefined
```

## call / apply

> 作用：改变this指向

> 区别：传参列表的形式不同

> call：第一个传 this 指向，后续则是构造函数的参数

```js
let Person = function(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
    // 实际就是将这里的 this 指向变更为 obj
    // 例如：obj.name = name
}
let obj = {}
Person.call(obj, 'hehe', 19, 'man');
// 访问 obj.name 返回 'hehe'
// 实际就是借助它人来生产自己
```

> apply 第一个传 this 指向，第二个参数传一个类数组，该数组即为传递的参数

```js
// 借用其他构造函数来生产自己
let Father = function(name, age) {
    this.name = name;
    this.age = age;
}
let Person = function (sex) {
    Father.apply(this, ['hehe', 19]);
    this.sex = sex;
}
let person = new Person('man');
// 访问 person.name 返回 'hehe'
// 和 call 唯一的区别就是传参列表的形式不同
// apply 是要以一个类数组的形式传递参数
```

## 继承发展史

> 传统形式 => 原型链，过多继承了无用属性

> 借用构造函数 => 不能继承借用构造函数的原型，每次构造函数都要多走一个函数

> 共享原型 => 不能随便改动自己的原型，因为和其他公用一个原型

```js
let Person = function(from) {
    this.from = 'china';
}
Person.prototype = {
    money: 'many'
}
let Me = function(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Me.prototype = Person.prototype;
let me = new Me('hehe', 19, 'man');
// 缺点 不能随便改动自己的原型
// 例如 Me.prototype.money = null;
// 那么 Person.prototype.money 返回 null
// 共有原型指向同一空间 不可随意更改
```



> 圣杯模式 => 使用一个构造函数作为中间层，解决共享原型缺点

```js
let Person = function(from) {
    this.from = 'china';
}
Person.prototype = {
    money: 'many'
}
let F = function() {}
F.prototype = Person.prototype; // 中间层构造函数
let Me = function(name, age, sex) {
    this.name = name;
    this.age = age;
    this.sex = sex;
}
Me.prototype = new F(); // 通过 new F 充当中间层
let me = new Me('hehe', 19, 'man');
// 通过 F构造函数作为中间层解决共享原型缺点
// 例如 Me.prototype.money = null;
// 那么 Person.prototype.money 依旧返回 'many'
```

> 封装圣杯模式共享原型

```js
let inherit = (function () {
    var F = function () { }
    return function (Origin, Target) {
        F.prototype = Target.prototype;
        Origin.prototype = new F();
        // 当需要时调用constructor该方法让其能找到构造器
        Origin.prototype.constructor = Origin;
        // 当需要时调用方法让其能找到它的超类 真正继承谁的
        Origin.prototype.uber = Target.prototype;
    }
}());

// 使用
let Father = function (money) {
    this.money = money;
}
Father.prototype = {
    surname: 'he'
}
let Me = function (name, age) {
    this.name = name;
    this.age = age;
}
inherit(Me, Father);
let me = new Me('hehe', 19);
// Me 的原型继承 Father 的原型 
```

## 枚举对象

> 访问属性的两种方式

- obj.name => 内部隐式 obj['name']
- obj['name'] => 注意使用字符串

- 使用 for in 枚举对象

```js
let obj = {
    name: 'hehe',
    age: 19,
    sex: 'man'
}
let newObj = {}
for(let prop in obj) {
    newObj[prop] = obj[prop];
}
// 遍历对象，每次把其属性名放进prop中
// 对象内有多少个属性则循环多少次 每次循环都将改变prop里的值
// 其prop里存的值为字符串类型
// 此处不使用点的方式访问属性是因为
// 是因为 obj.prop 会识别成访问 obj里的prop属性 
// 这样obj里又没有prop属性 就会返回 undefined
```

> hasOwnProperty

- 判断是否是自身的属性
- 可以用来剔除原型链上的属性

```js
// 此处会遍历到其原型链上的书写
let Obj = function(name, age) {
    this.name = name;
    this.age = age;
}
Obj.prototype = {
    surname: 'he'
}
let obj = new Obj('hehe', 19);
let newObj = {}
for(let prop in obj) {
    newObj[prop] = obj[prop];
}
// newObj.surname 返回 ‘he’
```

- 剔除继承原型链上的属性

```js
// hasOwnProperty 返回 true / false
// 是自己的属性返回 true 非自己的属性(原型继承的)返回 false
// hasOwnProperty 传递的必须是一个字符串 恰好 prop 内存的就是字符串
let Obj = function(name, age) {
    this.name = name;
    this.age = age;
}
Obj.prototype = {
    surname: 'he'
}
let obj = new Obj('hehe', 19);
let newObj = {}
for(let prop in obj) {
    // 是自己的属性才会进入此if
    if(obj.hasOwnProperty(prop)) {
        newObj[prop] = obj[prop];
    }

}
```

> in 操作符 仅作了解，基本不用

```js
// 查看该对象能不能访问到该属性 返回 true / false
let obj = {
    name: 'hehe',
    age: 19
}
console.log('name' in obj); // true
```

> instanceof

```js
// A instanceof B
// A 对象 是不是 B 构造函数构造出来的
// 看 A 原型链上 有没有 B 的原型
// 返回 true / false
let Test = function() {}
Test.prototype = {
    name: 'hehe'
}
let test = new Test();
console.log(test instanceof Test); // true
```

## this 指向

```js
1. 函数预编译过程 this --> window

2. 全局作用域里 this --> window

3. call / apply 可以改变函数运行时 this 指向

4. 谁调用它即指向谁
```

## 浅层克隆

```js
let clone = function(origin, target) {
    for(var prop in target) {
        if(target.hasOwnProperty(prop)) {
            origin[prop] = target[prop];
        }
    }
}

// 测试
let obj = {
    name: 'hehe',
    age: 19
}
let newObj = {}
clone(newObj, obj);
```

## 深层克隆

> 使用递归方式：

> 1. 判断是不是原始值

> 2. 判断是数组还是对象

> 3. 建立相应的数组或对象

```js
// 利用 Object.prototype.toString 判断是数组还是对象
let deepClone = function (origin, target) {
    let toStr = Object.prototype.toString;
    for (var prop in target) {
        if (target.hasOwnProperty(prop)) {
            if (target[prop] !== 'null' && typeof (target[prop]) == 'object') {
                if (toStr.call(target[prop]) == '[object Array]') {
                    origin[prop] = [];
                } else {
                    origin[prop] = {};
                }
                deepClone(origin[prop], target[prop]);
            } else {
                origin[prop] = target[prop];
            }
        }
    }
}

// 测试
let obj = {
    name: 'hehe',
    age: 19,
    arr: [{test:0},'a']
}
let newObj = {}
deepClone(newObj, obj);
```

## 类数组

- 可以利用属性名模拟数组的特性
- 可以动态的增长 length 属性
- 如果强行让类数组调用 push 方法，则会根据 length 属性值的位置进行属性的扩充
- 长得像数组但就不是数组，没有数组 push 等方法
- 类数组必须的：
	- 属性为索引（数字）属性
	- 必须有length属性 
	- 最好加上 push 方法（不加也可以使用）

```js
var obj = {
    1 : 'a',
    2 : 'b',
    3 : 'c',
    length : 3,
    push : Array.prototype.push,
    splice : Array.prototype.splice
    // 加上 splice 方法 自此就长得和数组一样了
}

// obj
// {1: 'a', 2: 'b', 3: 'c', length: 3, push: ƒ}

// obj.push('d')

// obj
// {1: 'a', 2: 'b', 3: 'd', length: 4, push: ƒ}
```
> 类数组内部原理

```js
Array.prototype.push = function (target) {
	this[this.length] = target; // obj[obj.length] = target;
	this.length ++; // obj.length ++;
}
```

> 根据 length 所在位置进行填充或覆盖

```js
var obj = {
    "2" : 'a',
    "3" : 'b',
    "length" : 2,
    "push" : Array.prototype.push,
    "splice" : Array.prototype.splice
}
obj.push('c');
obj.push('d');
// 访问 obj 
// 返回 [空属性 × 2, 'c', 'd', push: ƒ, splice: ƒ]
// length 为 4
```

> 类数组的用途

```js
既有对象特性又有数组特性
var obj = {
    "0" : 'a',
    "1" : 'b',
    "2" : 'b',
    "length" : 3,
    name : 'abc',
    age : 123,
    "push" : Array.prototype.push,
    "splice" : Array.prototype.splice
}
```

## 数组去重

-  es5 其中一个方法
- 利用对象的特性
- 对象不可能有两个同名的属性
- 把数组的每位放进对象里当做属性值

```js
var arr = [1,1,1,1,2,2,2,3,3,1,2,3,'a','b','a','a',0,0];

Array.prototype.unique = function () {
    var temp = {},
        arr = [],
        len = this.length;
    for(var i = 0; i < len; i ++) {
        if(!temp[this[i]]) {
            temp[this[i]] = 1;
            arr.push(this[i]);
        }
    }
    return arr;
}

var newArr = arr.unique();
```

## try catch

- 捕获错误信息，但是不中断代码块外后续代码执行
- 当 try 代码块中出现一个错误时会进行错误捕获
- 捕获的错误信息会以一个错误对象传入 catch 参数中

```js
try{
    console.log('a');
    console.log(b); // 第二行出错，不影响该代码块外后续代码
    console.log('c');

}catch(e) { // e --> error 是个对象 error.message error.name
    // 捕捉错误信息
    // 信息储存在参数里
    // try 里面代码不出错则不执行 catch
    // 当 try 内有错误时则执行 catch 并且允许操作错误信息

    console.log(e);
    // ReferenceError: b is not defined
    // at cs.html:85:21

    console.log(e.name);
    // ReferenceError

    console.log(e.message); 
    // b is not defined  
}
console.log('hehe'); // 不会阻断后续代码
```

## 错误信息

> Error.name 的六种值对应的信息

- EvalError ：eval() 的使用与定义不一致
- RangeError ：数值越界
- ReferenceError ：非法或不能识别的引用数值
- SyntaxError ：发送语法解析错误
- TypeError ：操作数类型错误
- URIError ：URI 处理函数使用不当

## es5 严格模式

> "use strict"  写在逻辑的最顶端 即前面可以有注释 空格 回车 换行

> 开启后将不在兼容 es3 的一些不规则语法 使用全新的 es5 规范

> 两种模式 全局模式、局部模式（推荐）

- 就是一行字符串，不会对不兼容严格模式的浏览器产生影响
- 不支持 with 和 arguments.callee 和 fun.caller
- 变量赋值前必须声明
- 局部 this 必须被赋值（Person.call(null/undefined) 严格模式预编译为 undefined
- 拒绝重复属性和参数（重复形参等）
- es3.0 和 es5.0 产生冲突的部分使用 es5.0

## String 对象

> String 对象的常用属性和方法

> String() 转为字符串类型

- 将传入的值转换为字符串类型 任何数据类型都可以转为字符串类型

> length   
>
> 字符串的长度 静态属性

- 语法：**str.length**

- 注意：js中的字符串底层是基于数组的
- 对于一些不常用的特殊字符计算出来的长度会与实际不符合 
- 具体原因为表示字符的编码不同 例如 "𝌆" 得出的长度就为 2 

```js
let let x = 'abc';
let y =  x.length;
console.log(y + ' ' + typeof y); // 3 number
```
> charAt() 
>
> 从一个字符串中返回指定的字符

- 语法：**str.charAt(index)**
- 注意：  默认索引位为 0 溢出查询返回一个空字符串

```js
let x = 'abc';
let y = x.charAt(1);
console.log(y + ' ' + typeof y); // b string
```

> String.prototype.charCodeAt() 
>
> 返回指定字符在 Unicode 编码表中的位置

- 语法：**str.charCodeAt(index)**
- 注意：  返回的是 0 到 65535 之间的整数； 
  - 查询的索引位溢出则返回 NaN；

```js 
let x = 'abc';
let y = x.charCodeAt(0);
console.log(y + ' ' + typeof y); // 97 number
```

> String.prototype.concat() 
>
> 拼接字符串 将多个字符串拼接返回一个新的字符串

- 语法：**str.concat(str2,strN)**
- 注意：不改变原数据 返回一个新的字符串
  - 对于性能 官方强烈建议使用赋值操作符（+, +=）代替 concat 方法

```js
let x = 'abc';
let x2 = 'def';
let y = x.concat(x2);
console.log(y + ' ' + typeof y); // abcdef string
```

> String.prototype.endsWith() [es6] 
>
> 确定一个字符串是否在另一个字符串的末尾

- 语法：**str.endsWith(str [,len])**
  - str 字符串
  - len 指定长度[可选]
- 注意：在指定一个长度中 这个字符串是否以该字符串结尾
  - 该方法对大小写敏感 返回结果为布尔值

```js
let x = 'abcdefg';
let y = x.endsWith('bc',3);
console.log(y + ' ' + typeof y); // true boolean
```

> String.fromCharCode() 
>
> 将 Unicode 编码数字转为字符

- 语法：**String.fromCharCode(index,indexN)**
- 注意： 更多用法查阅文档

```js
let x = 'abcdefg';
let y = String.fromCharCode(97, 98);
console.log(y + ' ' + typeof y); // ab string
```

> String.prototype.includes() [es6] 
>
> 判断一个字符串中是否含有另一个字符串

- 语法：**str.includes(str[, position])**

- 注意：大小写敏感
  - 第一个参数为需要匹配的字符串
  - 第二个为开始索引位[选填] 默认为 0
  - 返回结果为布尔值

```js
let x = 'abcdefg';
let y = x.includes('bcd'); // x 里面是否有 bcd
console.log(y + ' ' + typeof y); // true boolean 
```

> String.prototype.indexOf() 
>
> 匹配该值第一次出现的位置

- 语法：**str.indexOf(searchValue [, fromIndex]) **
  - searchValue 查找的值
  - 开始的索引位
- 注意：大小写铭感
  - 第一个参数为需要查找的值 第二个参数开始查找的索引位[选填] 默认为 0
  - 匹配成功返回匹配成功开始的索引位 失败则返回 -1
  - 第二个参数若小于匹配仓库的长度[负数]时 则当做 0 处理
  - 若超出[大于]匹配仓库的长度则作匹配失败处理 匹配的最终返回值为 -1
  - 若匹配一个空字符其返回值将会有‘奇怪’的结果，详情查阅文档

```js
et x = 'abcdefg';
let y = x.indexOf('c');
console.log(y + ' ' + typeof y); // 2 number
```

> String.prototype.lastIndexOf() 
>
> 从最后开始匹配该值第一次出现的位置

- 语法：**str.lastIndexOf(searchValue[, fromIndex])**
- 注意：大小写铭感 
  - 从后面开始往回匹配 成功返回索引位 失败返回 -1
  - 小于匹配仓库的长度[负数]时 作匹配失败 返回 -1
  - 超出[大于]匹配仓库的长度则 依旧匹配成功 因自后往回匹配
  -  若匹配一个空字符其返回值将会有‘奇怪’的结果，详情查阅文档

```js
let x = 'abccdefg';
let y = x.lastIndexOf('c');
console.log(y + ' ' + typeof y); // 3 number
```

> String.prototype.slice() 
>
> 提取字符串的片断

- 语法：**str.slice(beginIndex[, endIndex])**
  - beginIndex 开始索引位
  - endIndex 结束索引位

- 注意：不改变原字符串
  - 第一位为初始截取位，第二位为最终截取位；[可负数]
  - 若为负数 则采用 length + 负数 转换为正数
  -  第二个参数若为空 则从第一个参数开始截取 截取到最后

```js
let x = 'abcdefg';
let y = x.slice(1, 3);
console.log(y + ' ' + typeof y); // bc string  
```

> String.prototype.split() 
>
> 字符串以何种方式分割转为数组

- 语法：**str.split([separator[, limit]])**
  - separator 分割的字符形式
  - limit 分割后的数量

- 注意：不改变原数组
  -  可不填参数[不建议]
  -  第一个参数 转换成数组的分割形式 例如 '-' ' ' ',' 甚至 '123' [可正则]
  - 第二个参数 限制分割后的数量（长度） [number]

```js
let x = 'a-b-c-d-e-f';
let y = x.split('-');
console.log(y + ' ' + typeof y); 
// ['a', 'b', 'c', 'd', 'e', 'f'] 'object'
```

> String.prototype.startsWith() [es6] 
>
> 确定一个字符串是否以另一个字符串的开头

- 语法：**str.startsWith(searchString[, position])**
- 注意：大小写敏感
  - 第一个参数为需要查询的字符串
  - 第二个参数为开始的索引为[可选] 默认为 0
  - 返回结果为布尔值

```js
let x = 'abcdefgh';
let y = x.startsWith('abc');
console.log(y, typeof y); // true 'boolean'
```

> String.prototype.substring() 
>
> 截取一个字符串

- 语法：**str.substring(indexStart[, indexEnd])**
- 注意：不改变原字符串
  - 第一个参数为截取初始位
  - 第二个参数为截取末端位[可选] 为空则截取后面所有
  -  参数如果为负数 或者NaN 则作为 0 处理

```js
let x = 'abcdefgh';
let y = x.substring(2, 3);
console.log(y, typeof y); // c string
```

> String.prototype.toLowerCase() 
>
> 将字符串转为小写

- 语法：**str.toLowerCase()**
- 注意：不改变原字符串

    let x = 'ABCdef';
    let y = x.toLowerCase();
    console.log(y, typeof y); // abcdef string

> str.toUpperCase() 
>
> 将字符串转为大写

- 语法：**str.toLowerCase()**
- 注意：不改变原字符串

```js
let x = 'ABCdef';
let y = x.toUpperCase();
console.log(y, typeof y); // ABCDEF string
```

> String.prototype.trim() 
>
> 删除字符串两端的空白

- 语法：**str.trim()**
- 注意：  不改变原字符串

```js
let x = '  abcde  ';
let y = x.trim();
console.log(y, typeof y); // abcde string
```

> String.prototype.trimEnd() 
>
> 删除字符串末端空白字符

- 语法：**str.trimEnd()**

- 注意：不改变原字符串

```js
let str = 'abc  ';
console.log(str.trimEnd()); // abc
```

> String.prototype.trimStart() 
>
> 删除字符串开头空白字符

-  语法：**str.trimStart()**

- 注意：不改变原字符串

```js
let str = '  abc';
console.log(str.trimStart()); // abc
```

> String.prototype.valueOf() 
>
> 返回 String 对象的原始值

- 语法：**str.valueOf()**
- 注意：不改变原字符串
  - 一个new后的字符串对象可以通过该方法转为原始字符串

```js
let x = new String('abc');
let y = x.valueOf();
console.log(y, typeof y); // abc string
```

> 文档地址：
> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String

## 正则表达式

```js
RegExp 对象(构造函数) （正则表达式）
作用：匹配特殊字符或特殊搭配的字符；

正则表达式上的方法 test => RegExp.test 返回 true/false
字符串上的方法 match => str.match(reg) 返回匹配内容 失败返回 null

正则表达式字面量：
        // 检测 str 里有没有 abc (reg规则) 返回布尔值
        let reg = /abc/;        
        let reg = /abc/;
        let str = 'abcdef';
        console.log(reg.test(str)); // true

正则表达式字面量属性：
        // 最后斜杠所写的表示正则的属性 例如：i g m
        // 可以多个属性以前组合 例如：ig
        let reg = /abc/i; // ignoreCase 忽略大小写
        let reg1 = /abc/g; // global 全局匹配
        let reg2 = /abc/m; // 多行匹配


正则表达式构造函数：
        let reg = new RegExp('abc');
        let str = 'abcdef';
        console.log(reg.test(str)); // true

正则表达式构造函数属性：
        // 属性书写在第二个参数
        // 可以多个属性以前组合 例如：ig
        let reg = new RegExp('abc', 'i');
        let reg = new RegExp('abc', 'g');
        let reg = new RegExp('abc', 'm');

内部可放正则表达式：
        let reg = new RegExp('abc');
        let reg1 = new RegExp(reg);

前面若没有添加new则使用的是引用 指向同一空间：
        // 无用知识
        let reg = /abc/;
        let reg1 = RegExp(reg);

字符串方法：
1. String.prototype.match()
        // 没有添加属性只返回一个匹配
        let reg = /abc/;
        let str = 'abcabcabcabc';
        console.log(str.match(reg)); 
        // ['abc', index: 0, input: 'abcabcabcabc', groups: undefined]

        // 添加属性 g 将所有匹配到的都返回
        let reg = /abc/g;
        let str = 'abcabcabcabc';
        console.log(str.match(reg));
        // ['abc', 'abc', 'abc', 'abc']

匹配以什么开头：
        // 使用 ^
        let reg = /^a/g;
        let str = 'abcabcabcabc';
        let z = str.match(reg);
        console.log(z); // ['a']

当添加多行匹配后使用 ^ :
        // 使用转义字符 \n 换行 + m 多行匹配可获得多个
        let reg = /^a/gm;
        let str = 'abcabc\nabcabc';
        let z = str.match(reg);
        console.log(z); // ['a', 'a']

表达式：
        // 每个表达式规则以一个 [] 形式存在 每一个 [] 匹配一个位置
        // 匹配三个位置 每个位置存在 0 - 9 （即以三个数字开头）
        // 每一个 [] 匹配一个位置 => 一个表达式代表一位
        let reg = /[0123456789][0123456789][0123456789]/g;
        let str = '2378rgd1242vfg234';
        let z = str.match(reg);
        console.log(z); // ['237', '124', '234']

        // 第一个位置存在 a / b 第二个位置存在 c / d 第三个位置存在 d
        let reg = /[ab][cd][d]/g;
        let str = 'abcd';
        let z = str.match(reg);
        console.log(z); // ['bcd']        

        简写表达式：
        // 按照asc码去排列
        [0-9] 0 到 9
        [a-z] a 到 z
        [0-9A-Za-z] 0 到 9 A 到 Z a 到 z
        [0-9A-z] 0 到 9 大A 到 小z
        
        // 当 ^ 在表达式中称为 非 => [^]
        // [^a][^b] 第一位不是a 第二位不是b
        let reg = /[^a][^b]/g;
        let str = 'abcdef';
        let z = str.match(reg);
        console.log(z); // ['bc', 'de']

另一种表达式：
        // | 或 需放在 () ()叫做子表达式 内
        let reg = /(abc|bcd)/g;
        let str = 'abcdef';
        let z = str.match(reg);
        console.log(z); // ['abc']

元字符(实际另一种表达式)：
        // \w 也代表一位
        // world => \w
        // \w === [0-9A-z_] => 字母
        // \W === [^\w] => 相反取补集
        // \d === [0-9] => 数字
        // \D === [^\d]
        // . === [^\r\n]

        // \b === 单词边界
        let reg = /\bcde/g;
        let str = 'abc cde fgh';
        let z = str.match(reg);
        console.log(z); // ['cde']
        // ......
        // 表达式内可以写元字符

量词：
        // 正则表达式匹配原则 贪婪匹配 能多不少
        // n+ => n 作为变量 + 表示是可重复出现一次到无数次 1 - Infinity
        // n* => 0 - Infinity
        // n? => 0 - 1

        // n{x} => 匹配 x 个 填 number
        let reg = /\w{2}/g; // 单词匹配
        let str = 'aaaaaaaaaa';
        let z = str.match(reg);
        console.log(z); // ['aa', 'aa', 'aa', 'aa', 'aa']

        // n{x,y} => 区间匹配 x - y ; y若省略则表示 Infinity

        // ^n 以 n 开头
        // n$ 以 n 结尾
        // /^abc$/g 以 abc 开头，并且以[这个] abc 结尾 达到限制字符串作用

        // /^d|$d/g 首或位含有数字
        // /^d[\s\S]*$d/g 首和尾都含有数字 中间拿区间拉伸

正则表达式对象的属性：(无大用)
        // global  RegExp 对象是否具有标志 g true / false
        // ignoreCase  RegExp 对象是否具有标志 i true / false
        // lastIndex  一个整数，标示开始下一次匹配的字符位置 true / false
        // multiline  RegExp 对象是否具有标志 m true / false
        // source  正则表达式的源文本（显示写的内容）

正则表达式对象的方法：
        // test  检索字符串中指定的值 返回 true 或 false
        // exec  检索字符串中指定的值 返回找到的值 并确定其位置 [重点]
        // 由 lastIndex 的游标[索引]控制 [可以手动更改]
        let reg = /ab/g;
        let str = 'abababab';
        console.log(reg.lastIndex); // 0
        console.log(reg.exec(str)); // ['ab', index: 0, input: 'abababab', groups: undefined]
        console.log(reg.lastIndex); // 2
        console.log(reg.exec(str)); // ['ab', index: 2, input: 'abababab', groups: undefined]
        console.log(reg.lastIndex); // 4
        console.log(reg.exec(str)); // ['ab', index: 4, input: 'abababab', groups: undefined]
        console.log(reg.lastIndex); // 6
        console.log(reg.exec(str)); // ['ab', index: 6, input: 'abababab', groups: undefined]
        console.log(reg.lastIndex); // 8
        console.log(reg.exec(str)); // null
        console.log(reg.lastIndex); // 0
        console.log(reg.exec(str)); // ['ab', index: 0, input: 'abababab', groups: undefined]

正则表达式子表达式：
        // () 当放在括号内时会对其进行记录值
        // /(a)\1/g  \1表示反向引用第一个子表达式里面的内容 => 匹配 a和后面同样的a
        // /(\w)\1\1\1/g 匹配一个同样字符出现4次 例如 aaaa bbbb
        // /(\w)\1(\w)\2/g 匹配 aabb 形式出现的字符 

支持正则表达式的 String 方法：
        // search  检索与正则表达式相匹配的值 // 返回匹配到的位置 （非 -1） 则表示匹配成功 -1 表示失败
        // match  找到一个或多个正则表达式的匹配
        // replace  替换与正则表达式匹配的子串 [重要]
        let reg = /a/g;
        let str = 'aa';
        console.log(str.replace(reg, 'b')); // bb

        let reg = /(\w)\1(\w)\2/g;
        let str = 'aabb';
        console.log(str.replace(reg, '$2$2$1$1')); // bbaa 在第二个参数中也能反向引用到 使用$

        let reg = /(\w)\1(\w)\2/g;
        let str = 'aabb';
        console.log(str.replace(reg, function($, $1, $2) {
                return $2 + $2 + $1 + $1 + 'abc';
        })); // $ 匹配的元数据 $1 - $2 反向引用会放入形参内 依次传 系统帮我们调用多次函数

        // split  把字符串分割为字符串数组

        小例子：
        // 将 the-first-name 变成小驼峰式
        let reg = /-(\w)/g;
        let str = 'the-first-name';
        console.log(str.replace(reg, function($, $1) {
            return $1.toUpperCase();
        }));

正向预查（正向断言）：
        // ?=
        let reg = /a(?=b)/g;
        let str = 'abaaaaa';
        console.log(str.match(reg)); // ['a']
        // 选中一个后面跟着一个b的a  b在此仅作修饰 起限定作用

非正向预查（正向断言）：
        // ?!
        // ?!b 即后面不是跟着b的a

非贪婪匹配：
        在任何一个量词的后面加上一个 ? 即可打破贪婪匹配
        let str = 'aaaaa';
        let reg = /a+?/g;
        console.log(str.match(reg)); // ['a', 'a', 'a', 'a', 'a']
        // 贪婪匹配则返回 ['aaaaa']
```

> 正则表达式参考目录：
> https://www.w3school.com.cn/jsref/jsref_obj_regexp.asp

## 转义字符

> 在使用时将转义字符放在字符串内

```html
示例：  '\n'

常用转义字符：

\0      空字符

\'      单引号

\"      双引号

\\      反斜杠

\n      换行
```

## Number 对象

> Number() 
> 将值转换为数字类型 转换失败返回 NaN
> 注意：  NaN 和 Infinity / -Infinity 都属于数字类型

> 常用属性和方法：

> Number.isNaN() 
> 确定传递的值是否是 NaN (非数)

- 语法：**Number.isNaN(value)**
- 注意： Number('abc') <==> NaN，将传递的值转为数字类型再同 NaN 比对
	- 兼容版本应使用全局的 isNaN()
	- 返回布尔值
```js
let x = 'abc';
console.log(Number.isNaN(x)); // true
```

> Number.isInteger() 
>
> 判断一个数是否为整数

- 语法：**Number.isInteger(value)**
- 注意：需确保传入的值为数字类型 否则永远为 false
  - 其内部并不会将其隐式转换为数字类型

```js
let x = 123.456;
console.log(Number.isInteger(x)); // false
```

> Number.parseFloat() 
>
> 将字符串解析成正常浮点数（小数）

- 语法：**Number.parseFloat(value)**
- 注意：忽略字符串两端空白 从第一位开始识别数字位 包括第一个小数点
  - 后面遇到非数字位则停止 转化不成则返回 NAN 或 Infinity
  - 兼容版本应使用全局的 parseFloat()

```js
let x = '123.456.789';
let y = Number.parseFloat(x);
console.log(y + ' ' + typeof y); // 123.456 number 
```

> Number.parseInt(string,[2-36]) 
>
> 将字符串转换为[整数]或[不同进制数]

- 语法：**Number.parseInt(string [,2-36]) **
- 注意：一个参数将其转换为整数 结果为数字类型 转换失败返回 NaN
  - 当两个参数时：将第二个参数作为第一个参数的进制数 
  - 将其转为 10 进制
  -  第一个传递值若非字符串内部将隐式转换为字符串
  - 可用于浮点数取整，进制转换
  - 最终转换后的类型为数字类型 失败返回 NaN
  - 第二个参数的范围为 2 - 36 即 0 和 1 进制被认为无意义
  - 36为数字（0 - 9） + 字母（a - z）最大表示数
  - 兼容版本应使用全局的 parseInt()

```js
let x = 'a';
let y = Number.parseInt(x,16);
console.log(y + ' ' + typeof y); // 10 number
```

> Number.prototype.toString([2-36]) 
>
> 将十进制数转为对应基底的进制数 默认基底为10

- 语法：**num.toString([2-36])**
- 注意：不传递参数默认为十进制 则仅将其转为字符串
  - 若传递值 需为 2 - 36 将调用者当做十进制，将传递的值作为进制基底
  -  Number 对象覆盖了 Object.prototype 对象上的 toString() 方法
  - 调用者的数据类型[必须]为[数字类型] 转换后的结果的类型为字符串类型

```js
let x = 12;
let y = x.toString(16);
console.log(y + ' ' + typeof y); // c string
```

> Number.prototype.toFixed() 
>
> 保留几位小数

- 语法：**num.toFixed([num])**
- 注意：保留几位小数 保留位若无则以 0 补充 1.toFixed(2) ==> 1.00
  - 保留的小数为[四拾伍入] 结果的类型为字符串类型
  - 有限制最多保留多少位小数，各个浏览器不同

```js
let x = 12.345;
let y = x.toFixed(2);
console.log(y + ' ' + typeof y); // 12.35 string  
```

> 文档地址：  
> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number

## Window 对象

> `window` 对象表示一个包含 DOM 文档的窗口，其 `document` 属性指向窗口中载入的 [DOM 文档](https://developer.mozilla.org/zh-CN/docs/Web/API/Document) 。
>
> `window`作为全局变量，代表了脚本正在运行的窗口，暴露给 Javascript 代码。
>
> 以下为 Window 常用属性和方法

> window.innerHeight
>
> 返回浏览器视口高度

- 语法：**window.innerHeight**
-  注意：该属性为只读
  - 返回的高度值包含滚动条
  - 返回的值不带单位
  - 返回的是一个整数

> window.innerWidth
>
> 返回浏览器视口宽度

- 语法：**window.innerWidth**
- 注意：该属性为只读
  - 返回的宽度值包含滚动条
  - 返回的值不带单位
  - 返回的是一个整数

> Window.outerHeight
>
> 获取整个浏览器窗口的高度

- 语法：**Window.outerHeight**
- 注意：该属性只读
  - 包括侧边栏（如果存在）、窗口镶边，和窗口调正边框
  - 即当前页面以为那些导航栏，搜索栏也是包括的

> Window.outerWidth
>
> 获取整个浏览器窗口的宽度

- 语法：**Window.outerWidth**
- 注意：该属性只读
  - 包括侧边栏（如果存在）、窗口镶边，和窗口调正边框
  - 即当前页面以为那些导航栏，搜索栏也是包括的

> Window.pageXOffset
>
> 返回页面水平方向滚动条滚动的像素值

- 语法：**Window.pageXOffset**
- 注意：该属性只读
  - 返回页面水平方向滚动条滚动的像素值
  - 返回值不带单位，该值有可能会是小数
  - `pageXOffset` 属性是 `scrollX` 属性的别名
  - 为了兼容还是使用 `pageXOffset`

> Window.pageYOffset
>
> 返回页面垂直方向滚动条滚动的像素值

- 语法：**Window.pageYOffset**
- 注意：该属性只读
  - 返回页面水平方向滚动条滚动的像素值
  - 返回值不带单位，该值有可能会是小数
  - `pageYOffset` 属性是 `scrollY` 属性的别名
  - 为了兼容还是使用 `pageYOffset`

> Window.screenLeft
>
> 返回浏览器左边界到操作系统桌面左边界的水平距离

- 语法：**Window.screenLeft**
- 注意：该属性只读
  - 返回浏览器左边界到操作系统桌面左边界的水平距离
  - 返回值不带单位
  - `screenLeft` 只是 `Window.screenX` 属性的别名，两者都可使用
  - 缩小窗口后再查看

> Window.screenTop
>
> 返回浏览器上边界到操作系统桌面上边界的水平像素距离

- 语法：**Window.screenTop**
- 注意：该属性只读
  - 返回浏览器上边界到操作系统桌面上边界的水平像素距离
  - 返回值不带单位
  - `screenTop` 只是 `Window.screenY` 属性的别名，两者都可使用
  - 缩小窗口后再查看

> window.alert(str)
>
> 显示一个可确认的警告对话框

- 注意：传入的值只能为字符串类型，非字符串类型将隐式转换

> window.confirm(str)
>
> 显示一个具有一个可确定和取消的模态对话框

- 注意：传入的值只能为字符串类型，非字符串类型将隐式转换
  - 确认返回值为 true 取消返回值为 false

> window.getSelection()
>
> 返回一个 [`Selection`](https://developer.mozilla.org/zh-CN/docs/Web/API/Selection) 对象，表示用户选择的文本范围或光标的当前位置。

- 注意：当执行该函数后会返回一个Selection对象
  - 该对象记录了用户选择的文本范围或光标的数据
  - 该方法调用String方法后可以得到用户鼠标所框选的文本内容
  - 可通过连接一个空字符串（""）或使用String() 或调用toString() 方法转换

> window.print()
>
> 打开[打印对话框]功能窗口，提示是否打印当前文档

> window.prompt
>
> 弹出一个可输入的对话框

- 语法：**result = window.prompt(text, value);**
  - `result` 用来存储用户输入文字的字符串，或者是 null。
  - `text` 用来提示用户输入文字的字符串，如果没有任何提示内容，该参数可以省略不写。
  - `value` 文本输入框中的默认值，该参数也可以省略不写。

> Window.scroll()
>
> 滚动（定位）窗口至文档中的特定位置

- 语法：
- **window.scroll(x-coord, y-coord);**
- **window.scroll(options);**
	- options 是一个包含三个属性的对象：
	- top 等同于 y-coord
	- left 等同于 x-coord
	- behavior 表示滚动行为，支持参数： 
	- smooth (平滑滚动)
	- instant (瞬间滚动)
	- 默认值 auto，效果等同于 instant
  
```js
// 垂直滚动（定位）到200像素那个位置
window.scroll(0,200); 
// 传递对象方式并且平滑滚动
window.scroll({
    top: 200,
    left: 0,
    behavior: 'smooth'
});
```

> Window.scrollTo()
>
> 滚动（定位）窗口至文档中的特定位置

- 语法：
- **window.scrollTo(x-coord, y-coord);**
- **window.scrollTo(options);**
	- options 是一个包含三个属性的对象：
	- top 等同于 y-coord
	- left 等同于 x-coord
	- behavior 表示滚动行为，支持参数： 
	- smooth (平滑滚动)
	- instant (瞬间滚动)
	- 默认值 auto，效果等同于 instant
  
- `window.scrollTo` 和 `window.scroll` 一致
```js
// 垂直滚动（定位）到200像素那个位置
window.scrollTo(0,200); 
// 传递对象方式并且平滑滚动
window.scrollTo({
    top: 200,
    left: 0,
    behavior: 'smooth'
});
```

> Window.scrollBy()
>
> 滚动窗口至文档中的特定位置

- 语法：
- **window.scrollBy(x-coord, y-coord);**
- **window.scrollBy(options);**
	- options 是一个包含三个属性的对象：
	- top 等同于 y-coord
	- left 等同于 x-coord
	- behavior 表示滚动行为，支持参数： 
	- smooth (平滑滚动)
	- instant (瞬间滚动)
	- 默认值 auto，效果等同于 instant
  
- 注意：该方法是在原有滚动距离上增加的
```js
// 垂直滚动增加200像素
window.scrollBy(0,200); 
// 传递对象方式并且平滑滚动距离增加200像素
window.scrollBy({
    top: 200,
    left: 0,
    behavior: 'smooth'
});
```

> Window.stop()
>
> 该方法的效果相当于点击了浏览器的停止按钮。
>
> 由于脚本的加载顺序，该方法不能阻止已经包含在加载中的文档，但是它能够阻止图片、新窗口、和一些会延迟加载的对象的加载。

> window.setTimeout()
>
> 延时定时器

- 语法：
- **var timeoutID = scope.setTimeout(function[, delay, arg1, arg2, ...]);**
- **var timeoutID = scope.setTimeout(function[, delay]);** `正常使用该条语法`
- **var timeoutID = scope.setTimeout(code[, delay]);**
  - function 回调函数，到达时间调用
  - code 不推荐 有风险 和eval() 一样
  - `delay` [可选] 延迟的时间 单位毫秒 默认为 0
  - `arg1, ..., argN` [可选] 附加参数，一旦定时器到期，它们会作为参数传递给`function`
- 注意：清除该定时器使用 clearTimeout(timeID);
  - 将定时器的唯一标识符放入即可清除

> window.setInterval()
>
> 循环定时器

- 语法：
- **var intervalID = setInterval(func, [delay, arg1, arg2, ...]);**
- **var intervalID = setInterval(function[, delay]);**
- **var intervalID = setInterval(code, [delay]);**
  - function 回调函数，到达时间调用
  - code 不推荐 有风险 和eval() 一样
  - `delay` [可选] 间隔的时间 单位毫秒 默认为 0
  - `arg1, ..., argN` [可选] 附加参数，一旦定时器到期，它们会作为参数传递给`function`

- 注意：清除该定时器使用 clearInterval(timeID);
  - 将定时器的唯一标识符放入即可清除

> Window.getComputedStyle()
>
> 查询元素最终渲染后的样式

- 语法：**let style = window.getComputedStyle(element, [pseudoElt]);**

  - element 需要获取的元素
  - pseudoElt [可选] 指定一个要匹配的伪元素的字符串。必须对普通元素省略（或`null`）
- 注意：该方法只读
  - 返回这个元素的样式表 当前元素一切css的显示值（计算后的值）无添加值 即为默认值


```js
// 示例
let elm = document.documentElement;
window.getComputedStyle(elm,null).width;
// 或者
 window.getComputedStyle(elm,'after')['width'];
```

## Document 对象

> document 对象被挂载到 window 上，所以 window.document 是可以访问的
>
> 以下为 document 的常用属性和方法

> document.documentElement
>
> 获取 html 元素

> document.body
>
> 获取 body 标签

> document.head
>
> 获取第一个 head 标签

> document.createElement(elmName)
>
> 创建一个标签

> document.getElementById(idName)
>
> id 选择器

> document.getElementsByClassName(className)
>
> class 选择器 返回的是一个类数组

- 注意：该方法实际继承自 Element

  - 所以你可在 dom 元素上使用该方法以达到限制选择范围

  - 可以多个 class一起并列选择

  ```html
  <div class="a b"></div>
  <script>
  document.getElementsByClassName('a b'); // 也可获取到
  </script>
  ```

> document.getElementsByName(name)
>
> name 名选择器

- 注意：只有部分标签 name 可生效（表单，表单元素，img，iframe）

> document.getElementsByTagName(tagName)
>
> 标签名选择器 返回的是一个类数组

- 注意：该方法实际继承自 Element
- 所以你可在 dom 元素上使用该方法以达到限制选择范围

> document.querySelector(selectors)
>
> 静态选择器 以 css 选择器方式选择元素

- 注意：以 css 选择器方式选择元素
  - 选择的是第一个匹配的元素，匹配采用深度优先
  - 其所选择出来的是一个副本，并非实时的
  - 即当你删除这个元素时，它依然保存之前的(副本)
  - 该方法实际继承自 Element
  - 所以你可在 dom 元素上使用该方法以达到限制选择范围

> document.querySelectorAll(selectors)
>
> 静态选择器 以 css 选择器方式选择元素

- 注意：以 css 选择器方式选择元素
  - 选择出来的是一个类数组，匹配采用深度优先
  - 其所选择出来的是一个副本，并非实时的
  - 即当你删除这个元素时，它依然保存之前的(副本)
  - 该方法实际继承自 Element
  - 所以你可在 dom 元素上使用该方法以达到限制选择范围

> document.createDocumentFragment()
>
> 创建一个文档碎片，插入文档不会触发回流，可以优化性能

## Node 对象

> 各种类型的 DOM API 对象会从这个接口继承
>
> 以下为 Node 的常用属性和方法

> Node.parentNode
>
> 返回父节点，最顶端的 parentNode 为 #document，只读

> Node.childNodes
>
> 返回子节点集合，以类数组出现，只读

> Node.firstChild
>
> 返回第一个子节点，只读

> Node.lastChild
>
> 返回最后一个子节点，只读

> Node.nextSibling
>
> 返回后一个兄弟节点，只读

> Node.previousSibling
>
> 返回前一个兄弟节点，只读

> Node.nodeName
>
> 返回当前节点的名称，只读

> Node.textContent
>
> 返回该节点及其后代的文本内容，代码书写的文本，没有空白折叠过的
>
> 使用 `textContent` 可以防止 [XSS 攻击](https://developer.mozilla.org/zh-CN/docs/Glossary/Cross-site_scripting)

> Node.nodeType
>
> 返回当前节点的类型，只读

- 常用类型有：
  - 1 元素节点
  - 2 属性节点
  - 3 文本节点
  - 8 注释节点
  - 9 document 文档
  - 11 documentFragment 文档片段（碎片）

> Node.parentElement
>
> 返回父元素节点，只读

> Node.appendChild()
>
> 在该节点内的最后插入一个节点（通常为元素节点）

- 注意：如果该节点已被插入而后再插入将会剪切之前已被插入的
  - 正确做法是使用 `node.cloneNode([deep])` 克隆一个新的
  - 插入的只能为一个创建出来的节点，不可以是字符串自行书写的节点
  - 一次只能插入一个，新api `Element.append`() 更多新功能


> Node.cloneNode()
>
> 克隆一个节点

- 语法：**let clone =  node.cloneNode([deep]);**
  - node 将要被克隆的节点
  - deep [可选] 是否采用深度克隆，
  - 如果为 `true`，则该节点的所有后代节点也都会被克隆，
  - 如果为 `false`，则只克隆该节点本身。

> Node.compareDocumentPosition()
>
> 比较当前节点与任意文档中的另一个节点的位置关系，详细使用查阅文档

> Node.contains()
>
> 是否为该节点的后代节点

- 语法：**node.contains( otherNode )**
  - `otherNode` 是否是 node 的后代节点
- 注意：返回的是一个布尔值

> Node.hasChildNodes()
>
> 查看node节点是否有子节点，返回true则有1个或多个子节点；返回false则没有子节点

> Node.insertBefore()
>
> 在该节点之前插入一个节点

- 语法：**ParentNode.insertBefore(a, b)**
  - insert a , Before b ，将 a 放到 b 的前面
- 注意：读法 insert a , Before b
  - 通过父节点插入 将 a 放到 b 的前面
  - 一定要父节点调用
  - 如果该节点已被插入而后再插入将会剪切之前已被插入的
  - 正确做法是使用 `node.cloneNode([deep])` 克隆一个新的

> Node.removeChild()
>
> 删除一个指定子节点。返回删除的节点，实际是剪切操作

- 语法：
- **let oldChild = element.removeChild(child);**
- **element.remove();**
  - `child` 要移除的那个子节点
  - `node` 是`child`的父节点
  - oldChild 保存对删除的子节点的引用。`oldChild` === `child`
  - 第一种语法为父节点删除子节点（谋杀），是剪切（保存这个引用）
  - 第二种是自身调用方法删除（自杀），是完全删除（取消引用被GC清理）

> Node.replaceChild()
>
> 替换当前节点的一个子节点

- 语法：**parentNode.replaceChild(newChild, oldChild);**
  - **`newChild`**用来替换 `oldChild` 的新节点。
  - 如果该节点已经存在于 DOM 树中，则它首先会被从原始位置删除。
  - **`oldChild`**被替换掉的原始节点。

## Element 对象

> 以下为 Element 的常用属性和方法

> Element.attributes
>
> 返回该元素所有属性节点，以类数组出现

> Element.childElementCount
>
> 返回该元素的子元素节点个数，只读

> Element.children
>
> 返回该元素的子元素节点们，只读

> Element.classList
>
> 返回该元素的所有class类名，以类数组出现，es6新方法

- 该属性上还有四个方法：
- add() 添加类，可添加多个（类似push）
- remove() 删除指定类，可删除多个
- replace(oldToken, newToken) 
  - 替换类如果第一个参数 token 在列表中不存在， 
  - `replace()` 立刻返回`false` ，而不会将新 token 字符串添加到列表中。
  - 返回值 true 替换成功，false 替换失败
- toggle(token, [force]) 
  - 一个参数，删除一个指定标记的类
  - [force] 默认为 true 
  - 如果为 `true`，当这个需要删除的类不存在的话则将这个不存在的类添加。
  - 如果为 `false`，当这个需要删除的类不存在则不进行操作。
  - 返回值：布尔值：`true` 表示该标记的类存在class列表中，`false` 不存在列表中

> Element.className
>
> 返回该元素类名（字符串），可修改，es5旧方法

> Element.clientHeight
>
> 获取该元素的（padding box）的高度，内容 + padding ，只读

- 注意：高度为 内容 + padding

  - 不包括 margin、border、滚动条
  - 对于块盒是获取其css设置的高（没设置时则是内容撑开的高）行块盒同块盒一致
  - 对于行盒无法获取高度，即使内容撑开的也无法获取
  - 获取的值是一个整数，如果是小数将会被四拾伍入

  - 在根元素（`<html>` 元素）或怪异模式下的 `<body>` 元素上使用 `clientHeight` 时，

  - 该属性将返回视口高度（不包含任何滚动条），这是一个特例。

> Element.clientWidth
>
> 获取该元素的（padding box）的宽度，内容 + padding ，只读

- 注意：高度为 内容 + padding

  - 不包括 margin、border、滚动条
  - 对于块盒是获取其css设置的宽（没设置时则是内容撑开的宽）行块盒同块盒一致
  - 对于行盒无法获取宽度，即使内容撑开的也无法获取
  - 获取的值是一个整数，如果是小数将会被四拾伍入

  - 在根元素（`<html>` 元素）或怪异模式下的 `<body>` 元素上使用 `clientHeight` 时，

  - 该属性将返回视口高度（不包含任何滚动条），这是一个特例。

> Element.clientLeft
>
> 获取元素左边框宽度，如果左边有滚动将加上滚动条的宽，只读

> Element.clientTop
>
> 获取元素上边框的宽度，只读

> Element.firstElementChild
>
> 返回第一个子元素，只读

> Element.lastElementChild
>
> 返回最后一个子元素，只读

> Element.nextElementSibling
>
> 返回后一个兄弟元素节点，只读

> Element.previousElementSibling
>
> 返回前一个兄弟元素节点，只读

> Element.id
>
> 获取元素的 id ，该属性可写，赋值会覆盖已经存在的

> Element.innerHTML
>
> 获取元素内部的所有值，包括 html、文本，该属性可写，赋值会覆盖已经存在的

- 使用不当会存在安全问题，插入纯文本推荐使用 Node.textContent

> Element.tagName
>
> 获取元素的标签名，html中返回的是大写

> Element.scrollHeight
>
> 获取元素的高度，包括溢出不可见的（隐藏或者可见的超出文字也算）

- 注意：包括 padding 和 伪元素 ，但是不包括边框、滚动条、外边距
  - 如果存在滚动条那其得出的值将会是减去滚动条的高
  - 得到的数如果非整数将被四拾伍入

```html
<style>
    .test {
        width: 100px;
        height: 100px;
        background-color: lightblue;
    }

    .child {
        width: 50px;
        height: 120px;
        background-color: #008c8c;
        overflow: auto;
        font-size: 15px;
        white-space: nowrap;
    }
</style>
<div class="test" id="cs">
    <div class="child">
        这是一段测试文本
    </div>
</div>
<script>
    let $ = (dom) => {
        return document.querySelector(dom);
    }
    let test = $('.test');
    let child = $('.child');
    console.log(child.scrollHeight);  // 本是120 实际得出 101
</script>
```

> Element.scrollWidth
> 获取元素的高度，包括溢出不可见的（隐藏或者可见的超出文字也算）

- 注意：包括 padding 和 伪元素 ，但是不包括边框、滚动条、外边距
  - 如果存在滚动条那其得出的值将会是减去滚动条的宽
  - 得到的数如果非整数将被四拾伍入
  - 具体特点同 `Element.scrollHeight`

> Element.scrollLeft
>
> 获取元素内的滚动距离，可写

- 注意：如果元素不能滚动（比如：元素没有溢出，滚动条无法使用），那么`scrollLeft` 的值是 0
  - 在缩放的屏幕中得到的值有可能是小数
  - 如果设置一个超出界限的值，它最终的值也只能等于那个界限，所以可以直接设置一个最大/最小来快速达到边界值
  - 它计算的值是内部内容被滚动了多少（内容被拉动多少距离），而不是滚动条的那个距离
  

```html
<style>
    .test {
        width: 100px;
        height: 100px;
        background-color: lightblue;
        overflow: auto;
    }
    
    .child {
        width: 50px;
        height: 50px;
        background-color: #008c8c;
    }
</style>
<div class="test" id="cs">
    <div class="child">
        Lorem ipsum, dolor sit amet consectetur adipisicing elit. Voluptates hic fugiat qui
        tenetur odio quisquam eveniet itaque dolorem incidunt nisi necessitatibus odit, 
        pariatur, porro assumenda aliquid. Eveniet ducimus nobis facilis ad, eaque quam
        nostrum veritatis, reprehenderit pariatur, ullam dolorum ratione quod corrupti 
        voluptatum ea hic eligendi molestias animi explicabo. Nulla?
    </div>
</div>
<script>
    let $ = (dom) => {
        return document.querySelector(dom);
    }
    let test = $('.test');
    let child = $('.child');
    console.log('test.scrollTop: ' + test.scrollTop);
    console.log('test.scrollLeft: ' + test.scrollLeft);
</script>
```

> Element.scrollTop
> 获取元素内的滚动距离，可写

- 注意：如果元素不能滚动（比如：元素没有溢出，滚动条无法使用），那么`scrollTop` 的值是 0
  - 在缩放的屏幕中得到的值有可能是小数
  - 如果设置一个超出界限的值，它最终的值也只能等于那个界限，所以可以直接设置一个最大/最小来快速达到边界值
  - 它计算的值是内部内容被滚动了多少（内容被拉动多少距离），而不是滚动条的那个距离
  - 具体特点同 `Element.scrollLeft`

> Element.append()
>
> 在该元素内的最后插入一个节点

- 该方法允许插入字符串，但是字符串最终只会被当做文本节点写入，所以加入元素之类的节点还是得创建的才行
  - 支持同时添加多个节点
  - 没有返回值

> Element.hasAttribute()
>
> 判断该元素上指定的属性存不存在，返回布尔值

> Element.getAttribute(name)
>
> 获取该元素上指定属性的值

> Element.setAttribute(name,value)
>
> 给该元素添加一个 属性+值，如果该属性已存在，则进行修改

> Element.removeAttribute(name)
>
> 在该元素上删除一个指定属性

> Element.getAttributeNames()
>
> 返回该元素上所有属性的名称，以数组形式返回

> Element.getBoundingClientRect()
>
> 返回一个对象，提供了元素的大小及其相对于视口的位置

- 注意：该对象只读
  - 该对象除了 width、height 外都是相对视口的
  - width、height 包括了 padding 和 border

<img src="data:image/png;base64,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" alt="图" style="zoom:50%;" />

> Element.scroll()
>
> 在元素中，使其滚动条滚动到特定位置

- 语法：
- **element.scroll(x-coord, y-coord)**
- **element.scroll(options)**
- 注意：具体使用方式同 `window.scroll()` 方法一致 
  - 它计算的值是内部内容被滚动了多少（内容被拉动多少距离），而不是滚动条的那个距离


> Element.scrollTo()
>
> 在元素中，使其滚动条滚动到特定位置

- 语法：
- **element.scrollTo(x-coord, y-coord)**
- **element.scrollTo(options)**
- 注意：具体使用方式同 `window.scrollTo()` 方法一致 
  - 它计算的值是内部内容被滚动了多少（内容被拉动多少距离），而不是滚动条的那个距离

> Element.scrollBy()
>
> 在元素中，使其滚动条滚动一段距离

- 语法：
- **element.scrollBy(x-coord, y-coord)**
- **element.scroll(options)**
- 注意：具体使用方式同 `window.scrollBy()` 方法一致 
  - 滚动距离是叠加的，即调用该方法将加上之前已有的距离
  - 它计算的值是内部内容被滚动了多少（内容被拉动多少距离），而不是滚动条的那个距离

> 以上方法为常用的，还有更多的强大功能接口请查阅文档
>
> https://developer.mozilla.org/zh-CN/docs/Web/API/Element

## HTMLElement 对象

> 以下为 `HTMLElement` 对象的常用属性和方法

> HTMLElement.contentEditable
>
> 返回该元素是否可编辑，返回值有三个，只读

- 注意：
  - true 可编辑
  - false 不可编辑
  - inherit 继承了元素可编辑状态

> HTMLElement.isContentEditable
>
> 返回该元素是否可编辑，返回值为布尔值，只读

> HTMLElement.dir
>
> 获取该元素文本书写方向，返回值有两个，只读

- 注意：
  - `ltr` 从左到右
  - `rtl` 从右到左

> HTMLElement.innerText
>
> 获取该元素的文本内容，不同与 `innerHTML` ，该属性会自动排除非文本节点，可写

> HTMLElement.offsetHeight
>
> 返回该元素的像素高度，包含 padding、border、滚动条

- 注意：该属性只读
  - 返回值是一个整数，小数将会被四拾伍入
  - 设置了 display: none; 的元素返回值将为 0

> HTMLElement.offsetWidth
>
> 返回该元素的像素宽度，包含 padding、border、滚动条

- 注意：该属性只读
  - 返回值是一个整数，小数将会被四拾伍入
  - 设置了 display: none; 的元素返回值将为 0

> HTMLElement.offsetParent
> 返回最近的定位父级，如无，返回 body，只读

- 注意：body.offsetParent 返回 null
  - 该元素或其祖先元素的 `display: none;` 时，返回 null
  - 该元素 `position: fixed;` 时，返回 `null`

> HTMLElement.offsetLeft
>
> 返回该元素相对最近定位父级的相对位置（不论自身有无定位），只读

- 注意：原点为左上角
  - 对于无定位的父级元素，返回相对文档的坐标
  - 不论自身有无定位，都返回相对最近有定位父级的相对位置

> HTMLElement.offsetTop
>
> 返回该元素相对最近定位父级的相对位置（不论自身有无定位），只读

- 注意：原点为左上角
  - 对于无定位的父级元素，返回相对文档的坐标
  - 不论自身有无定位，都返回相对最近有定位父级的相对位置

> ETMLElement.click()
>
> 对该元素模拟一次点击事件

## DOM 结构树

```html
    -->  Document --> HTMLDocument

                   --> Text 文本
    -->  CharacterDate
                   --> Comment 注释
Node  
    -->  Element （文档中的元素） --> HTMLElement --> HTMLHeadeElement、HTMLBodyElement、HTMLDivElement 等

    -->  Attr


Document 可以把它看做一个对象 但你不能 new 它(new 了也没用) 是系统流光自己用的

Document 下有两个分支 HTMLDocument.prototype 和 XMLDocument.prototype

HTMLDocument 的方法继承自 HTMLDocument.prototype

XMLDocument 的方法继承自 XMLDocument.prototype

Document.prototype 的方法是 html 和 xml 的共性方法

document 的原型是 HTMLDocument.prototype

HTMLDocument.prototype 的原型是 Document.prototype

继承关系：

document --> HTMLDocument.prototype --> Document.prototype

补充：
  var x = document.getElementsByTagName('*');
  通配符选择器 选择所有元素
```

## Math 对象

> Math 和其他全局对象不同，它不是一个构造器
>
> 其内的属性和方法都是静态的它的里边封装了数学运算相关的属性和方法
>

> 以下为 `Math` 对象的常用属性和方法：

> Math.ceil() 对一个数向上取整 小数为只要有值就进1

> Math.floor() 对一个数向下取整 小数部分舍去

> Math.round() 对一个数进行四舍五入取整

> Math.random() 生成一个 0 - 1 之间的随机数 从0（包括0）往上，但是不包括1（排除1）

> Math.max() 返回多个数中的最大值 var max = Math.max(10,20,30);

> Math.min() 返回多个数中的最小值

> Math.pow(x,y) 返回 x 的 y 次方

> Math.sqrt() 开平方

> 文档地址：
> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Math

## Date 日期对象

> 使用该对象的属性和方法需要 new

- 语法：
    - new Date();
    - new Date(value);
    - new Date(dateString);
    - new Date(year, monthIndex [, day [, hours [, minutes [, seconds [, milliseconds]]]]]);
    - `year` 表示年份的整数值。 0 到 99 会被映射至 1900 年至 1999 年，其它值代表实际年份。
    - `monthIndex` 表示月份的整数值，从 0（1 月）到 11（12 月）
    - `day` 表示一个月中的第几天的整数值，从 1 开始。默认值为 1 ， [可选]
    - `hours` 表示一天中的小时数的整数值 (24 小时制)。默认值为 0（午夜） ， [可选]
    - `minutes` 表示一个完整时间（如 01:10:00）中的分钟部分的整数值。默认值为 0 ， [可选]
    - `seconds` 表示一个完整时间（如 01:10:00）中的秒部分的整数值。默认值为 0 ， [可选]
    - `milliseconds` 表示一个完整时间的毫秒部分的整数值。默认值为 0 ， [可选]

```js
// 实例对象
let date = new Date();

// 2022年9月9日10点10分10秒10毫秒
let date = new Date(2022, 8, 9, 10, 10, 10, 10);
```

> 注意：date对象里面的时间记录的是出生那一刻的时间。
>  后续方法访问的也是date对象出生那一刻的，而非实时访问当前的。

> 以下为 `Date` 对象的常用方法

> getFullYear() 返回年份。

> getMonth() 返回月份（从 0-11）。

> getDate() 返回月中的第几天（从 1 到 31）。

> getDay() 返回星期几（0-6）即本周当中的第几天，星期日为0。

> getHours() 返回小时（从 0-23）。

> getMinutes() 返回分钟（从 0-59）。

> getSeconds() 返回秒数（从 0-59）。

> getMilliseconds() 返回毫秒（0-999）。

> setFullYear() 设置日期对象的年份.

> setMonth() 设置日期对象的月份。

> setDate() 设置 Date 对象中月的某一天。

> setHours() 设置日期对象的小时。

> setMinutes() 设置日期对象的分钟数。

> setSeconds() 设置日期对象的秒数。

> setMilliseconds() 设置日期对象的毫秒数。

> setTime() 将日期设置为 1970 年 1 月 1 日之后/之前的指定毫秒数。

> 重要：
> getTime() 返回自 1970 年 1 月 1 日 0 时 0 分 0 秒 至经的毫秒数，也称为获取时间戳。

> 时间戳：记录当前这个时刻。 

```js
// 简单测量运行效率：
let firstTime = new Date();
for(let i = 0; i < 10000000; i++) {}
let lastTime = new Date();
console.log(lastTime - firstTime);
```

> 7个数字分别指定年、月、日、小时、分钟、秒、毫秒（按此顺序）

> 6个数字指定年、月、日、小时、分钟、秒

> 5个数字指定年、月、日、小时和分钟

> 4个数字指定年、月、日和小时

> 3 个数字指定年、月和日

> 2个数字指定年份和月份

> 注意：
> 1个参数会被认为是毫秒（从1970开始过了多少毫秒）

> 调用 toString 转成更容易读懂的日期格式

> 例如：Wed Mar 25 2015 08:00:00 GMT+0800 (中国标准时间)

> 在 HTML 中显示日期对象时，会自动调用 toString() 方法自动转换为字符串。

> 毫秒转换：
>  一天 = 24小时
>  1小时 = 60分钟
>  1分钟 = 60秒
>  1秒 = 1000毫秒
> 1分钟 = 1000 * 60
>  1小时 = (1000 * 60) * 60
>  1天 = ((1000 * 60) * 60) * 24
> 时间差 / 1000 转换的秒
>  时间差 / 1000 % 60 转成分后剩余的秒数
>  时间差 / 1000 / 60 % 60 转成小时后剩余的分数

> 文档地址：
>
> https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Date

## 脚本化 css

> 读写元素css
> element.style.prop

> 可对鞋行间样式。没有兼容性问题。碰到 float 这样的保留子属性，前面加 css
> 例：float --> cssFloat

> 复合属性必须拆解，组合单词书写必须小驼峰式
> 写入的值必须是字符串格式

## Event 事件对象

> 事件指的是在系统和用户交换之间产生的状态，可能由系统触发，也有可能由用户触发
>
> 例如鼠标点击，鼠标移动，敲下键盘等一系列交互行为都被称为事件

> 绑定使用有两种方式：

> 句柄方式：重复绑定同一事件将会被覆盖

- dom.on + type
- <elm on+ type = js></elm>

> addEventListener()：重复绑定同一事件，全都执行

- addEventListener(type, listener);
- addEventListener(type, listener, options);
- addEventListener(type, listener, useCapture);
  - `type` 监听的事件类型
  - `listener` 监听触发的回调
  - `options` 一个指定有关 `listener` 属性的可选参数对象 [可选]
  - `options` {[capture], [once], [passive], [signal], [useCapture]}
    - `once` 一个布尔值，表示 `listener` 在添加之后最多只调用一次。如果为 `true`，`listener` 会在其被调用之后自动移除
    - 剩余不常用则不作介绍，具体查阅文档。


```html
<div class='test'></div>
<script>
    let $ = (dom) => {
        return document.querySelector(dom);
    }
    let test = $('.test');
    test.addEventListener('click', function(e) {
    console.log(e.target);
	},{
    	captrue: true,
    	once: true
	});
</script>
```

> 当事件被触发时会产生一个 `event` 对象，记录了触发该事件时的一系列数据
>
> 以下为常用对象参数：

> Event.bubbles
>
> 返回一个布尔值，表明当前事件是否会向 DOM 树上层元素冒泡

> Event.cancelable
>
> 返回一个布尔值，表明该事件是否可以取消

> Event.target
>
> 触发事件的对象 触发事件对象的索引 ，可以用来做事件委托

> Event.type
>
> 返回该事件的类型

> 继承自 `Event` 对象，根据其衍生的还有诸多事件，例如 `FocusEvent` `Input` 等
>
> 以下为常用的事件类型：

### Event

> 以下为直接继承自 `Event` 的事件类型

> scroll
>
> 滚动条滚动时触发，该事件不会冒泡；

> load
>
> 当文件加载完成时触发，常用于 `外链`、`img`、`body`、`window` 上，并非每个元素都有该事件；

> change
>
> 当表单元素文本改变时且失去焦点时触发，该事件仅在表单元素上生效；

### FocusEvent

> 表单类
>
> 该类事件只有表单和设置了 `contenteditable` 的元素才会触发

> focus
>
> 元素焦点聚集时触发，该默认事件不可取消，不会冒泡；

> focusin
>
> 元素焦点聚集时触发，该默认事件不可取消，和 `focus` 的区别就是该事件会冒泡；

> blus
>
> 元素失去焦点时触发，该默认事件不可取消，不会冒泡；

> focusout
>
> 元素失去焦点时触发，该默认事件不可取消，和 `blus` 的区别就是该事件会冒泡；

### InputEvent

>表单类
>
>该类事件只有表单和设置了 `contenteditable` 的元素才会触发

> 常用属性：
>
> `data` 用户输入时触发事件时输入的内容，删除、粘贴操作无值

> input
>
> 元素输入或修改时触发，该事件会冒泡；

### KeyboardEvent

> 键盘类
>
> 该类事件只有表单和设置了 `contenteditable` 的元素，和绑定在 `docuemnt` 和 `windown` 上才会触发

> 常用属性：
>
> `code` 触发事件的物理按键值，返回的信息更多，包括物理按键的位置
>
> `key` 触发事件时的物理按键值
>
> `altKey` 是否按下了 `Alt` 按键，返回布尔值
>
> `ctrlKey` 是否按下了 `Ctrl` 按键，返回布尔值

> keydown
>
> 键盘按下时触发，该事件会冒泡；

> keyup
>
> 键盘抬起时触发，该事件会冒泡；

### MouseEvent

> 鼠标类
>
> 该事件在用户使用鼠标交互中触发

> 常用属性：
>
> `button` 按下时才会有值，返回值：0 鼠标左键、1 滚轮键、2 鼠标右键 ...
>
> `clientX` 触发事件时，鼠标相对视口的 X 位置
>
> `clientY` 触发事件时，鼠标相对视口的 Y 位置
>
> `offsetX` 触发事件时，鼠标离触发事件的对象的左上角的 X 距离 （包括padding，但不包括border）
>
> `offsetY` 触发事件时，鼠标离触发事件的对象的左上角的 Y 距离 （包括padding，但不包括border）
>
> `pageX` 触发事件时，鼠标相对文档的 X 距离
>
> `pageY` 触发事件时，鼠标相对文档的 Y 距离
>
> `screenX` 触发事件时，鼠标相对整个屏幕的 X 距离（屏幕 = 浏览器导航栏 + 浏览器视口 ...）
>
> `screenY` 触发事件时，鼠标相对整个屏幕的 Y 距离（屏幕 = 浏览器导航栏 + 浏览器视口 ...）

> click
>
> 元素被点击抬起后触发，`click` = `mousedown` + `mouseup` ，事件会冒泡；

> mousedown
>
> 元素点击时那一刻触发，该事件会冒泡；

> mouseup
>
> 元素点击时抬起那一刻触发，该事件会冒泡；

> dblclick
>
> 元素短时间内被单击两次时触发，该事件会被冒泡；

> mouseover
>
> 鼠标移入元素那一刻触发，该事件会冒泡；

> mouseent
>
> 鼠标移入元素那一刻触发，该事件不会冒泡；

> mouseout
>
> 鼠标移出元素那一刻触发，该事件会冒泡；

> mouseleave
>
> 鼠标移出元素那一刻触发，该事件不会冒泡；

> mousemove
>
> 鼠标在元素上移动时触发，持续触发，直到鼠标离开该元素，该事件会冒泡；

> contextmenu
>
> 鼠标右键出现菜单时触发，该默认事件行为可以被取消，在移动端项目中我们会进行取消；

### TouchEvent

> 触摸屏类
>
> 该事件在用户触摸屏幕时触发（移动端）

> 常用属性：
>
> 该事件继承了 Event
>
> <a href="https://developer.mozilla.org/zh-CN/docs/Web/API/Touch" traget="_blank">MDN文档</a>
>
> touches 一个列表对象，包含当前所有接触屏幕的触点
>
> 待补充

> touchstart
>
> 一个或多个触摸点触碰屏幕那一刻触发，该事件会冒泡；

> touchend
>
> 当触点离开屏幕那一刻触发，该事件会冒泡；

> touchmove
>
> 触摸屏幕时触发该事件，持续触发，直到触点离开屏幕，该事件会冒泡；

> touchcancel
>
> 触点被中断时触发（弹窗、离开文档窗口、超出设备最大触点），该事件会冒泡；

### WheelEvent

> 滚动类
>
> 该事件在用户交互滚动时触发

> wheel
>
> 当鼠标滚轮滚动时触发，可以设置在 可以滚动元素、body、html、document、window上，该事件会冒泡；

### 取消绑定事件

> 注意：若绑定匿名函数，则无法解除。

> 句柄
> elm.onclick = false / '' / null;

> addEventListener
> elm.removeEventListener(type,fun,false);

> 兼容ie
> elm.detachEvent('on' + type,fun);

### 取消默认事件

> 默认事件 -- 表单提交刷新，a标签跳转，右键菜单等

> return false; 以对象属性的方式注册的事件才生效

```js
// 例如右键出菜单事件：
document.oncontextmenu = function () {
  return false; // 阻止 兼容性很好 但只有句柄方式绑定的才好使
}
```

> event.preventDefault() w3c标准，ie9以下不兼容

```js
// 例如右键出菜单事件：
document.addEventListener('contextmenu',function (e) {
  e.preventDefault();
});
```

> event.returnValue = false 兼容ie

```js
document.addEventListener('contextmenu',function (e) {
e.returnValue = false;
});
```

> 封装阻止默认事件的函数 cancelHandler(event);

```js
function cancelHandler(event) {
  if(event.preventDefault) {
    event.preventDefault();
  }else {
    event.returnValue = false;
  }
}
```

### 事件处理模型

> 一个事件对象的事件模型只能为一个
> 即 要不冒泡 要不捕获

> 事件冒泡：（常规模型）
> 结构上（非视觉上）嵌套关系的元素，会存在事件冒泡功能，
> 即同一事件，自子元素冒泡向父级（自底向上）
> 例子：当点击子元素时会将这个点击也传递到父元素上

> 事件捕获：
> 结构上（非视觉上）嵌套关系的元素，会存在事件捕获的功能，
> 即同一事件，子父元素捕获至子元素（事件源元素 如：该点击触发的元素）（自顶向下）

> 开启捕获模型；

```js
dom.addEventListener('click',fun,true);
// 最后一个 false 改为 true
```

> IE没有捕获事件模型
> 触发顺序，先捕获，后冒泡
> focus，blur，change，submit，reset，select 等事件不冒泡

> 取消冒泡：
> w3c标准 event.stopPropagation() ie9以下不兼容

```js
dom.addEventListener('click',fun(e) {
  e.stopPropagation();
},false);
```

> ie独有：event.cancelBubble = true;

```js
dom.addEventListener('click',fun(e) {
  e.cancelBubble = true;
},false);
```

> 封装取消冒泡的函数 stopBubble(event);

```js
function stopBubble(event) {
  if(event.stopPropagation) {
    event.stopPropagation();
  }else {
    event.cancelBubble = true;
  }
}
```

## JSON 对象

> JSON 本质就是一个字符串，只不过该字符串是以一定的规律(对象形式)组成
>
> JSON 通常被用于数据传输，JSON 的两个方法：

> JSON.stringify(obj);
>
> 将对象转成 `JSON` 格式的字符串

> JSON.parse(JSON);
>
> 将 `JSON` 格式的字符串转为对象

## 页面渲染

> 浏览器解析页面
> `dom` 树（`domTree`） 深度优先原则
> 当遇到链接外部资源的 `dom` 时 如 `img` `iframe` 等
> 它只要识别了标签 就将其挂到 `dom`树 上，而链接的外部资源采用异步加载
> 当 `dom` 树 的完成 代表所有`dom` 节点的解析完毕，并不意味着 `dom` 加载完毕（`img` 外部资源等）

> 当`dom` 树完成后会等着 `css` 树（`cssTree`）解析 `css` 树也是深度优先
> 当 `css` 树也解析完成后 会将 `dom` 树 + `css`树 拼一起形成 = `randerTree`（渲染，绘制）树
> 当 渲染树完成后 渲染引擎才开始绘制页面 按照 渲染树 绘制

> 当`js` 对 `dom` 节点 添加，删除 或者 `dom`节点 宽高变化，位置变化，
> `display:none` --> `block`
> 或者一些特殊语法 `offsetWidth` `offsetHeight` 等时，
> 它就会重新构建(回流)渲染树，我们应该减少这样的低效操作
> 改一个颜色的话仅会触发重绘 重绘浪费效率较少

## 异步加载js

> js加载的缺点：
> 加载工具包（fun方法）会阻塞文档，过多的js会影响页面效率，
> 一旦网速不好，那么整个网站将等待js加载而不进行后续渲染等工作。
> 有些工具方法需要按需加载，用到再加载，不用不加载。

> 异步加载的三种方案：
> (1) w3c标准方法
> `async` 异步加载，加载完就执行，`async` 只能加载外部脚本，不能把js写在script里面。
> `<script src='' async='async'></script>` 

> (2) ie 方法
> `defer` 异步加载，但要等到dom文档全部解析完才会被执行。
> 只有ie能用，可以外部链接或者也可以将代码写到script内部（2选1）。
> 属性值等于属性名可省略属性值 ie9以下可以使用
> `<script src='' defer='defer'></script>` 

> 1 和 2 方法加载时不阻塞页面
> 3 方法在读取的过程中会阻塞页面，但由于代码只有几行可以忽略不计

> (3) 创建script，插入到dom中，加载完毕后 callBack。可达到兼容 可以按需加载
> 实际是利用 html 加载外部资源异步的方法

```js
var script = document.createElement('script');
// 当读到这一句时就会开始加载 是异步加载的
script.src = 'xxx.js';
// 当将dom插入到页面时才开始执行 否则仅下载完
document.head.appendChild(script);
```

> 何时才加载完？
> 很多事件上都会有一个 load 事件 下载事件也有

```js
var script = document.createElement('script');
// 当读到这一句时就会开始加载 是异步加载的
script.src = 'xxx.js';
// 当将dom插入到页面时才开始执行 否则仅下载完
script.onload = function () {
  // 当它下载完后才执行这里
  // xxx.js里的方法
}
document.head.appendChild(script);
```

> ie 的script上没有 load 事件
> ie方法：返回一个状态码
> 当为 'complete' 或者 'loaded' 时为加载完成

```js
script.onreadystatechange = function () {
  if(script.readyState == 'complete' || script.adyState == 'loaded') {
    // 当它下载完后才执行这里
    // xxx.js里的方法
  }
}
```

> 兼容性写法：

```js
var script = document.createElement('script');
// 当读到这一句时就会开始加载 是异步加载的
script.src = 'xxx.js';
// 当将dom插入到页面时才开始执行 否则仅下载完
if (script.readyState) {
    script.onreadystatechange = function () {
        if (script.readyState == 'complete' || script.adyState == 'loaded') {
            // 当它下载完后才执行这里
            // xxx.js里的方法
            test();

        }
    }
}else {
    script.onload = function () {
        // 当它下载完后才执行这里
            // xxx.js里的方法
            test();
    }
}
document.head.appendChild(script);
```

> 封装方法：

```js
function loadScript(url, callback) {
    var script = document.createElement('script');
    if (script.readyState) {
        script.onreadystatechange = function () {
            if (script.readyState == 'complete' || script.adyState == 'loaded') {
                callback();
            }
        }
    } else {
        script.onload = function () {
            callback();
        }
    }
    script.src = url;
    document.head.appendChild(script);
}
loadScript('demo.js',function () {
  // 直接传函数名会 no defined
  // demo.js里面的方法
  test();
  // 也可以跟里面的代码配合，不需要传递函数
  // 传递一个字符串 根据对象调用方法执行
});
```

## 编程理念

> 效率恐怖，代码风骚

> 深山老林，编程20年

> 学校不支持编程，已经辍学

> 媳妇不支持编程，已经离婚

> 父母不支持编程，已经断绝关系

> 孩子不支持编程，已经移送孤儿院

## es5结束

> 这并不是结束，而是刚刚开始
>
> 如果你学完以上内容，恭喜你以成功入门前端
