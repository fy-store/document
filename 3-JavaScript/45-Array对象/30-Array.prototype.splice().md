## Array.prototype.splice()

修改数组里的元素 . 该方法改变原数组 . 



**语法:**

```js
arr.splice(start [[, deleteCount] , item1, ..., itemN])
```



- `start`

  切口开始的位置, 默认为 0 , 如果为负数则使用 负数 + arr.length

- `deleteCount`

  删除的元素数量 , 把 start 位置作为 0 . 
  
- `item`

  从切口处增加的元素 . 



**返回值:**

被删除的元素片段 , 将被包装成数组 . 



**示例:**

```js
var arr = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
arr.splice(2, 3, 'a', 'b', 'c')
console.log(arr) // [0, 1, 'a', 'b', 'c', 5, 6, 7, 8, 9]
```

