## Array.prototype.filter()

该方法用于测试数组的每一项 , 通过测试的元素将被复制 . 复制为浅拷贝 . 不改变原数组 . 

该方法通常用于过滤和筛选 .



**语法:**

```js
arr.filter(callbackFn [, thisArg])
```



- `callbackFn`

  测试函数 , 开发者在该函数内对数据进行操作 , 返回一个布尔值用于指示当前元素是否通过测试 .
  
  只有通过测试的元素才会被拷贝 , 该测试函数会接收三个参数 . 
  
  - `element`
  
    当前测试中的元素
  
  - `index`
  
    当前测试元素在数组中的索引 .
  
  - `array`
  
    调用了 filter() 方法的本身 .

- `thisArg` [可选]

  测试函数的this指向



**返回值:**

一个拷贝后的新的数组 , 只有通过测试的元素才会被拷贝 , 不改变原数组 . 



**示例:**

```js
var arr = [1, 2, 3, 4, 5]
var result = arr.filter(function (elm) {
    return elm > 3
})
console.log(result) // [4, 5]
```

