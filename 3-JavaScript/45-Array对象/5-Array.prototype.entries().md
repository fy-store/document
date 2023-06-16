## Array.prototype.entries()

该方法返回一个迭代器 . 迭代器对象中以数组键值对存在  => [key, value] .



**语法:**

```js
var iterator = arr.entries()
```



**返回值:**

一个迭代器 .



**示例:**

```js
var arr = ['a', 'b', 'c', 'd', 'e']
var iterator = arr.entries()
console.log(iterator)

for (var i of iterator) {
    console.log(i)
}

// [0, 'a']
// [1, 'b']
// [2, 'c']
// [3, 'd']
// [4, 'e']
```

