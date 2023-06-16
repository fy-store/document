## Array.prototype.join()

将数组按指定方式拼接成一个字符串 .



**语法:**

```js
arr.join(separator)
```



- `separator`

  拼接方式 , 若省略将按照 `,` 拼接 , 如果数组项存在 undefined 和 null 将被转为空串 , 而非 'undefined' 和 'null'



**返回值:**

拼接后的字符串



**示例:**

```js
var arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
var result = arr.join('-')
console.log(result) // 0-1-2-3-4-5-6-7-8-9
```

