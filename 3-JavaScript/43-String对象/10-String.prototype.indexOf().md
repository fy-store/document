## String.prototype.indexOf()

返回给定字符串在当前字符串中第一次出现的下标(索引)



**语法:**

```js
str.indexOf(searchString [, position])
```



- `searchString`

  要查找的字符串

- `position`

  开始查找的位置



**返回值:**

所查找字符串在当前这个字符串中第一次出现的位置(下标/索引) , 如果不存在将返回 -1



**示例:**

```js
var str = 'abcde'
var result = str.indexOf('de', 2)
console.log(result) // 3
```

