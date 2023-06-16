## Array.prototype.push()

在数组末尾追加元素 , 该方法改变原数组 . 



**语法:**

```js
arr.push(element0, element1, /* … ,*/ elementN)
```



- `element`

  要追加的元素



**返回值:**

用方法的对象的新 length 属性 



**示例:**

```js
var arr = [0, 1, 2]
arr.push(3, 4, 5)
console.log(arr) // [0, 1, 2, 3, 4, 5]
```

