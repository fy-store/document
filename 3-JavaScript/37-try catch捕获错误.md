## try catch

[mdn文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/try...catch) 

try catch 用于捕获异常 , 由开发者自行决定是否抛出错误



**属性**

name: 原型上的属性 , 错误类型

message: 错误信息

stack: 错误堆栈信息, 具体出错的地方



**示例**

不确定代表是否报错时可将代码放入 `try` 语法块内 , 当发生错误时 `try catch` 语句会捕获错误

错误将走 `catch` 语法块 , 并且会传入一个错误对象 , 可通过 console.dir() 查看其具体属性

```js
try {
    console.log(a);
} catch (error) {
    console.log(error); 
    // ReferenceError: a is not defined
    // at deom.html:16:25
}
```



当你不需要使用错误对象时刻省略接受参数 , es6 支持省略 , 之前的版本不支持

```js
try {
    console.log(a);
} catch {}
```

