## Array.prototype.flatMap()

该方法让数组内的每一项依次执行一次处理函数 , 然后将结果展开一级 , 再将返回值放入新数组中 . 不改变原数组 . 

该方法相当于调用 map 后再调用 flat() 深度为 1 . 相当于是这两个方法的组合 . 



**语法:**

```js
arr.flatMap(callbackFn [, thisArg])
```



- `callbackFn`

  处理函数 , 返回值会被作为新数组的一项 . 该函数接收三个参数 .

  - `element`

    正则处理的元素

  - `index`

    正则处理元素在数组中的索引

  - `array`

    调用 `flatMap` 的数组

- `thisArg` [可选]

  处理函数的 this 指向



**返回值:**

一个处理后的新数组 . 



**示例:**

```js
var arr = [[1], [2, 3], 4, 5]
var result = arr.flatMap(function (item) {
    console.log(item); // (1) [1] , (2) [2, 3] , (3) 4 , (4) 5
    return item
})
console.log(result) // [1, 2, 3, 4, 5]
```

