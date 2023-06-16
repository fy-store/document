## String.prototype.isWellFormed()

该方法可以判断一个字符串中是否存在多个码元组成的码点(超出65535的字符)

通过这个方法我们就可以得知字符串的length是否等于字符的长度



**语法:**

```js
str.isWellFormed()
```



**返回值:**

布尔值



**示例:**

```js
var str = 'abc😄123'
var result = str.isWellFormed()
console.log(result) // true
```

