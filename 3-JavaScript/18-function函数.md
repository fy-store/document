## function函数

> 通过 function 定义一个函数

`function` 声明的函数分为*命名函数*(函数声明) , *函数表达式* , *匿名函数*



**命名函数:**

```js
function person() {}
```

函数声明将被作为一等公民

即命名函数将会在*预解析*过程中被提升至当前作用域的逻辑最顶端

*示例*

```js
console.log(person) // ƒ person() {}
function person() {}
```



**函数表达式:**

```js
var person = function person1() {}
```

当使用函数表达式时, 函数声明的命名将会被忽略, 并且函数表达式不会被提升

*示例*

```js
console.log(person) // undefined
var person = function person1() {}
typeof person1 // 'undefined'
```



**匿名函数:**

匿名函数即没有名字的函数

同样的匿名函数不会被提升

匿名函数不可直接定义, 需将匿名函数包装成表达式

可以通过一元正负中的 `+` `-` 或者小括号 `()` 

*示例*

```js
+function() {console.log(1)}
-function() {console.log(2)}
(function() {console.log(3)})
```





## 立即执行函数

> 立即执行函数也称为 IIFE

立即执行函数即当解析器读到该条函数语句时立即执行, 执行完毕后丢弃函数

通常立即执行函数用来做初始化, 或利用其闭包的特性来实现私有变量

```js
var num1 = +function() {console.log(1)}()
var num2 = -function() {console.log(2)}()
var num3 = (function() {console.log(3)})()
```


*官方推荐的写法*

```js
var num4 = (function() {
	console.log(3)
}()); // 执行小括号放在表达式里面 
```

