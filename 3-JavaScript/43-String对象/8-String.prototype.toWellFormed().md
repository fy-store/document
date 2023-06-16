## String.prototype.toWellFormed()

该方法可以对字符串中单独出现的不足以组成字符的码点使用Unicode中的 U+FFFD 进行替换

Unicode 中的  U+FFFD =>  `�`



**语法:**

```js
str.toWellFormed()
```



**返回值:**

一个替换后的新的字符串 , 不改变原始字符串



**示例:**

*示例1*

```js
var str = '\uD800'
var result = String.fromCharCode(str)
console.log(result) // '' 空字符串 , 因为无法组成字符
```



*示例2*

```js
var str = '\uD800'
var result = str.toWellFormed()
console.log(result)
```



*示例3*

```js
var str = 'abc😄\uD800ccc'
var result = str.toWellFormed()
console.log(result) // abc😄�ccc
```

