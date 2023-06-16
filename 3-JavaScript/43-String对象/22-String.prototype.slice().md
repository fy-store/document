## String.prototype.slice()

该方法用于截取字符串片段 . 不改变原字符串 , 返回一个新的字符串 .



**语法:**

```js
str.slice([beginIndex[, endIndex]])
```



- `beginIndex`

  开始位置 , 可以为负数 , 留空则为 0

- `endIndex` [可选]

  结束位置 , 可以为负数 , 留空则为 length - 1 (即字符串末尾)



**返回值:**

从原字符串中提取出来的字符串 . 



**示例:**

*示例1*

截取全部

```js
var str = '1234567890'
var result = str.slice()
console.log(result) // 1234567890
```



*示例2*

指定位置截取到末尾

```js
var str = '1234567890'
var result = str.slice(2)
console.log(result) // 34567890
```



*示例3*

指定位置截取至指定位置

```js
var str = '1234567890'
var result = str.slice(2, 3)
console.log(result) // 3
```

