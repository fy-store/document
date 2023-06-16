## Array.prototype.forEach()

该方法让数组的每一项依次执行一次处理函数 . 



**语法:**

```js
arr.forEach(callbackFn [, thisArg])
```



- `callbackFn`

  处理函数 , 返回值会被作为新数组的一项 . 该函数接收三个参数 .

  - `element`

    正则处理的元素

  - `index`

    正则处理元素在数组中的索引

  - `array`

    调用 `forEach` 的数组

- `thisArg` [可选]

  处理函数的 this 指向



**返回值:**

undefined



**示例:**

```js
var arr = [1, 2, 3, 4, 5]
arr.forEach(function (item, index) {
    arr[index] += 1
})
console.log(arr) // [2, 3, 4, 5, 6]
```

