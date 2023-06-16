## Array.prototype.slice()

截取数组片段 , 该方法不改变原数组 . 是一个复制行为 , 复制为浅拷贝 . 



**语法:**

```js
arr.slice([start [, end])
```



- `start` [可选]

  截取开始的位置 , 默认为 0 , 如果是负数则使用 负数 + arr.length

- `end` [可选]

  截取结束的位置 , 默认为数组末尾 , 如果为负数则使用 负数 + arr.length



**返回值:**

截取出来的片段, 会被包装成数组 . 



**示例:**

```js
var arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
var result = arr.slice(2, 5)
console.log(result) // [2, 3, 4]
```

