## Array.prototype.flat()

按指定深度递归该当前数组 , 将递归后的数组项依次放置到新数组中 , 返回一个新数组 . 不改变原数组 .

该方法属于复制行为 , 使用的是浅拷贝 , 可用于数组扁平化 . 



**语法:**

```js
arr.flat([depth])
```



- `depth` [可选]

  递归的深度 , 默认为 1



**返回值:**

递归后的新的数组



**示例:**

*示例1*

```js
var arr = [1, 2, [3, [4]], 5]
var result = arr.flat(1)
console.log(result) // [1, 2, 3, [4], 5]
```



*示例2*

使用一个相当大的数值 , 以保证数组全部扁平化

```js
var arr = [1, 2, [[3, 4, 5], 5], 5]
var result = arr.flat(10)
console.log(result) // [1, 2, 3, 4, 5, 5, 5]
```

