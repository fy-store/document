## String.prototype.includes()

判断给定字符串在当前字符串中是否存在 , 该方法区分大小写



**语法:**

```js
str.includes(searchString [, position])
```



- `searchString`

  要查找的字符串

- `position` [可选]

  开始查找的位置



**返回值:**

布尔值



**示例:**

```js
var str = 'abcde'
var result = str.includes('d', 2)
console.log(result) // true
```

