## Array.prototype.unshift()

在数组开头追加元素 , 该方法改变原数组 . 



**语法:**

```js
arr.unshift(element0, element1, /* … ,*/ elementN)
```



- `element`

  要追加的元素



**返回值:**

返回调用方法对象的新 length 属性



**示例:**

```js
var arr = [0, 1, 2]
arr.unshift(3, 4, 5)
console.log(arr) // [3, 4, 5, 0, 1, 2]
```

