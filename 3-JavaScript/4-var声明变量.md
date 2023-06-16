## var 声明变量

> var

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var" target="_blank">MDN文档</a> 

`var` 语句用于声明变量

var 语句可以连续声明多个变量, 也可在声明变量时初始化一个值 .



**语法:**

```js
var test1;
var test2 = 10;
var test3, test4;
var test3 = 'abc', test4 = [1, 2, 3];
```



**var 声明变量的特点:**

1. 变量提升
   - 使用 var 声明的变量会进行 `变量提升`
   - 在js的预解析过程中通篇扫描 将 var 声明的变量提升到逻辑的最顶端
2. 可重复声明
   - 重复声明的变量后面覆盖前面
3. 没有块级作用域
   - 在for循环等代码体中声明变量会被提升到全局，会造成变量泄漏而导致污染变量
4. 存在函数作用域



在es6之前变量声明只能使用 var , 在es6中新增了两个变量声明语句 , `let` 和 `const`

var 的变量提升发生在js代码正式执行前 , 具体发生在 `预解析` 中

var 变量提升时会将声明的变量提升到该作用域的逻辑最顶端 
