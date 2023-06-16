## Array.prototype.concat()

该方法用于合并多个数组 , 不改变原数组 , 返回一个新的合并后的数组 .

需要注意的是 , 这个合并数组只是一个浅拷贝 .



**语法:**

```js
arr.concat(arr0, arr1, ...)
```



- `arr1 ...`

  需要合并的数组



**返回值:**

一个合并后的新数组



**示例:**

```js
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var arr1 = ['a', 'b', 'c', 'd', 'e']
var result = arr.concat(arr1)
console.log(result) // [1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 'a', 'b', 'c', 'd', 'e']
```

