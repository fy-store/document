## Array.prototype.reduce()

该方法会让数组的每一项都执行一次处理函数 , 每次函数接收的第一个参数都是上一个函数的返回值 .

首次执行函数的第一个参数如果未指定初始值 , 则为数组的第0项 . 



**语法:**

```js
arr.reduce(callbackFn, initialValue)
```



- `callbackFn`

  处理函数 , 该函数接收四个参数 . 

  - `previousValue` 

    上一次调用 `callbackFn` 时的返回值 , 首次执行函数时若未指定初始值则为数组第0项 .

  - `currentValue`

    当前正则处理的元素, 首次执行函数时若未指定初始值则为数组第0项 , 如果指定了则为数组第1项 .

  - `currentIndex`

    正在处理的元素在数组中的下标 , 首次执行函数时若未指定初始值则为 0 , 如果指定了则为 1 . 

  - `array`

    调用 `reduce` 方法的数组 .

- `initialValue`

  初始值



**返回值:**

使用 “reducer” 回调函数遍历整个数组后的结果



**示例:**

```js
var arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
var result = arr.reduce(function (lastValue, value) {
    return lastValue + value
})
console.log(result) // 45
```

