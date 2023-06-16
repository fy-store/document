## Array.from()

该方法可以将一个可迭代对象或一个类数组转换成真正的数组 . 不改变原数组 . 

该方法是一个复制行为 , 复制为浅拷贝 . 

可迭代对象: 如 Map Set 或拥有迭代器的对象 . 



**语法:**

```js
Array.from(arrayLike [, mapFn [, thisArg]])
```



- `arrayLike`

  要转换的可迭代对象或类数组

- `mapFn` [可选]

  处理函数 , 如果设置了该参数 , 那么每个要添加到新数组的元素都会先经过一遍该函数 , 相当于 "中间件" , 该函数的返回值会作为新数组的元素 . 该函数会接收两个参数 . 

  - `element`

    当前正在处理的元素

  - `index`

    当前被处理元素在数组中的索引

- `thisArg` [可选]

  处理函数的 this 指向



**返回值:**

一个新的数组 . 



**示例:**

```js
var obj = {
    0: 'a',
    1: 'b',
    2: 'c',
    length: 3
}

var result = Array.from(obj)
console.log(result) // ['a', 'b', 'c']
```

