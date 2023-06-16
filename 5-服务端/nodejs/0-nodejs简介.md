# nodejs

> nodejs 是基于 Google v8引擎的一个 JavaScript 运行环境。
>
> node 提取了 JavaScript 的语法部分，并写入了一些自己的API，如操作文件、数据库等接口。
>
> 使得 node 能在服务器端中运行，让其足以媲美 PHP，Java 等后端语言。
>
> node 为 JavaScript 提供了服务器端的宿主环境，使得 JavaScript 可以开发后端。
>
> <a href="https://nodejs.org/en/" target="_blank">nodejs官网</a>

<hr>


nodejs的特点：

异步非阻塞的  I/O （I/O 线程池）

特别适合  I/O 密集型应用（适合高并发，但不适合CPU密集型）

事件循环机制

单线程 （优点亦是缺点）

跨平台

<hr>


> 名词解释

*广义上：*

I：input：输入设备，键盘，鼠标，摄像头等等

O：output：输出设备，显示器，打印机等



*计算机中：*

I/O：读写文件和数据库

以前：I/O 指读写文件

I：input：写

O：output：读

如今：I/O 指读写文件和读写数据库



I/O 密集型：频繁操作 I/O

CPU密集型：需要大量计算

<hr>

*nodejs的缺点：*

单线程

处理不好CPU密集型任务



## node函数特点

这些特点仅在使用 CommonJs 模块化时才会拥有, 当使用 es6 模块化标准时这些属性和方法不存在

> node 中的任何一个模块（js文件）都被一个外场所包裹
>
> 外层函数包裹的原因：
>
> 用于支持模块化语法
>
> 为了安全等原因 ，隐藏服务器内部实现 

<hr>


> 查看方法：

```js
console.log(arguments.callee.toString());
```

<hr>


> 提供的参数

- exports：用 于支持CommonJs模块化规范暴露语法

- require：用于支持CommonJs模块化规范的引入语法

- module：用 于支持CommonJs模块化规范暴露语法

- \__filename：当前运行文件的绝对路径

- \__dirname：当前运行文件所在目录的绝对路径



## node端js的组成部分

> 去掉了服务端不需要的，增加了服务端需要的API

去掉了 DOM BOM

去掉了全局对象 window ，增加了全局对象 global

node 中可以直接访问全局 global `console.log(global);`



