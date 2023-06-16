## Array.prototype.every()

对数组内的元素进行测试 , 看所有元素是否都通过测试 , 返回一个布尔值 .

该方法是一个迭代方法 , 其中只要有一个元素不能通过测试将直接返回 , 不再考虑后续元素 .



**语法:**

```js
arr.every(callbackFn [, thisArg])
```



- `callbackFn`

  用于测试的函数 , 开发者在该函数内对数据进行操作 , 返回一个布尔值用于指示当前元素是否通过测试 .

  该测试函数会接收三个参数 . 

  - `element`

    当前测试中的元素

  - `index`

    当前测试元素在数组中的索引 .

  - `array`

    调用了 every() 方法的本身 .

- `thisArg` [可选]

  测试函数的this指向



**返回值:**

布尔值 , 该数组的所有元素是否都通过测试 . 





**示例:**

```js
var arr = [1, 2, 3, 4, 5]
var result = arr.every(function (elm) {
    return elm > 0
})
console.log(result) // true
```

