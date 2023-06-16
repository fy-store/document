## String.prototype.startsWith()

判断当前字符串是否以一个指定的字符串开头 . 区分大小写 .



**语法:**

```js
str.startsWith(searchString[, position])
```



- `searchString`

  指定的字符串

- `position`

  开始查找的位置 , 默认值为 0



**返回值:**

布尔值



**示例:**

*示例1*

```js
var str = 'abcdefghi'
var result = str.startsWith('a')
console.log(result) // true
```



*示例2*

```js
var str = 'abcdefghi'
var result = str.startsWith('c', 2)
console.log(result) // true
```

