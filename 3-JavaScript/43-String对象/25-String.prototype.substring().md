## String.prototype.substring()

该方法用于提取字符串片段 , 不改变原字符串 . 

如果任一参数小于 0 或为 NaN，则被当作 0 .

如果任一参数大于 str.length，则被当作 str.length . 

总结就是不推荐使用负数 , slice 不会有这种情况 .



**语法:**

```js
str.substring([indexStart[, indexEnd]])
```



- `indexStart`

  开始的下标 , 若省略则为 0 .

- `indexEnd`

  结束的下标  , 这个参数可以省略 ,  一般而言都是 length - 1



**返回值:**

提取出来的字符串片段



**示例:**

```js
var str = 'abcdefghi'
var result = str.substring(3)
console.log(result) // defghi
```

