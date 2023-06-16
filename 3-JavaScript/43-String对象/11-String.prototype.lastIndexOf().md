## String.prototype.lastIndexOf()

返回给定字符串在当前字符串中第最后一次出现的下标(索引)

实际就是在查找过程中从后往前查找 .



**语法:**

```js
str.lastIndexOf(searchValue[, fromIndex])
```



- `searchValue`

  要查找的字符串

- `fromIndex`

  查找的范围



**返回值:**

所查找字符串在当前这个字符串中最后一次出现的位置(下标/索引) , 如果不存在将返回 -1



**示例:**

```js
var str = 'abcde'
var result = str.lastIndexOf('cd', 3)
console.log(result) // 2
```

