## Array.prototype.findLastIndex()

从数组后面开始往回查找 , 返回数组中从后往前中第一个通过测试的元素的下标 . 否则返回 -1



**语法:**

```js
 arr.findLastIndex(callbackFn [, thisArg])
```



- `callbackFn`

  测试函数 , 开发者在该函数内对数据进行操作 , 返回一个布尔值用于指示当前元素是否通过测试 .

  有通过测试的元素才会被返回 , 该测试函数会接收三个参数 . 

  - `element`

    当前测试中的元素

  - `index`

    当前测试元素在数组中的索引 .

  - `array`

    调用了 findLastIndex() 方法的本身 .

- `thisArg` [可选]

  测试函数的this指向



**示例:**

```js
 var arr = [1, 2, 3, 4, 5]
 var result = arr.findLastIndex(function (elm) {
     return elm > 0
 })
 console.log(result) // 4
```