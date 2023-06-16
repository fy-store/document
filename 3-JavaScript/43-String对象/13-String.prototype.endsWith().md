## String.prototype.endsWith()

判断给定字符串是否在当前字符串的末尾 , 该方法区分大小写



**语法:**

```js
str.endsWith(searchString[, length])
```



- `searchString`

  要查找的字符串

- `length` [可选]

  查找的范围 , 默认值为 `str.length`



**返回值:**

布尔值



**示例:**

```js
var str = 'abcde'
var result = str.endsWith('c', 3)
console.log(result) // true
```

