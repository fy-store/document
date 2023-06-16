## Array.prototype.indexOf()

返回给定元素在数组中第一次出现的下标 . 如果不存在将返回 -1 .



**语法:**

```js
arr.indexOf(searchElement [, fromIndex])
```



- `searchElement`

  需要查找的值

- `fromIndex` [可选]

  开始查找的位置 , 默认为 0 , 可以为负数 , 若为负数则为 fromIndex + array.length



**返回值:**

返回元素在数组中第一次出现的下标 , 不存在则返回 -1 .



**示例:**

```js
var arr = [1, 2, 3, 4, 5]
var result = arr.indexOf(3)
console.log(result) // 2
```

