## String.fromCodePoint()

静态方法返回使用指定的代码点序列创建的字符串

该方法和 String.fromCharCode() 类似



**语法:**

```js
String.fromCodePoint(num1[, ...[, numN]])
```



- `num`

   Unicode 编码位置，可以传递任意有效范围内的码点，包括大于 0xFFFF 的码点 .



**返回值:**

使用指定的 Unicode 编码位置创建的字符串



**示例:**

*示例1*

```js
String.fromCodePoint(65 ,66, 67) // 'ABC'
```



*示例2*

```js
var str = '😄'
var str1 = str.charCodeAt(0)
var str2 = str.charCodeAt(1)
var result = String.fromCodePoint(str1, str2)
console.log(result) // 😄
```

