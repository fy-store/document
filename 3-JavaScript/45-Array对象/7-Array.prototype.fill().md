## Array.prototype.fill()

该方法指定一个内容填充数组指定位置 . 该方法会改变原数组 . 

可使用负数 , 具体规则查看文档 . 



**语法:**

```js
arr.fill(value [, start [, end]])
```



- `value`

  填充的内容

- `start` [可选]

  填充的开始位置 , 默认为 0

- `end` [可选]

  填充的结束位置 , 默认为数组结束位置 , 该值即使超出数组项 , 依然只填充至数组结束位置 .



**返回值:**

一个填充后的数组 , 该方法是改变原数组 . 



**示例:**

*示例1*

```js
var arr = [1, 2, 3, 4, 5]
arr.fill(0, 3, 100)
console.log(arr) // [1, 2, 3, 0, 0]
```



*示例2*

配合 new Array() 使用

```js
var arr = new Array(10)
arr.fill(0)
console.log(arr) // [0, 0, 0, 0, 0, 0, 0, 0, 0, 0]
```

