## Array.prototype.map()

该方法让数组内的每一项依次执行一次处理函数 , 将返回值放入新数组中 . 不改变原数组 . 



**语法:**

```js
arr.map(callbackFn [, thisArg])
```



- `callbackFn`

  处理函数 , 返回值会被作为新数组的一项 . 该函数接收三个参数 .

  - `element`

    正则处理的元素

  - `index`

    正则处理元素在数组中的索引

  - `array`

    调用 `map` 的数组

- `thisArg` [可选]

  处理函数的 this 指向



**返回值:**

一个映射后的新数组 . 



**示例:**

```js
var arr = [1, 2, 3, 4, 5]
var result = arr.map(function (item) {
    return item + 1
})
console.log(result) // [2, 3, 4, 5, 6]
```

