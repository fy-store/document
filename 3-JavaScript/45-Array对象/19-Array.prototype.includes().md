## Array.prototype.includes()

该方法判断当前数组中是否存在一个指定值 . 这里指的是包含 . 

在该方法的判断中 NaN 可以被搜索到 , 但 +0 和 -0 被认为是相等 .



**语法:**

```js
arr.includes(searchElement [, fromIndex])
```



- `searchElement`

  需要查找的值

- `fromIndex` [可选]

  开始查找的位置 , 默认为 0 , 可以为负数 , 若为负数则为 fromIndex + array.length



**返回值:**

布尔值



**示例:**

```js
var arr = [1, 2, 3, 4, 5]
var result = arr.includes(3)
console.log(result) // true
```

