## String.prototype.replace()

该方法用于替换指定的字符串 . 一般这个方法配合正则表达式可以做到对字符串的全局替换 .

这个匹配模式可以是正则表达式也可以是字符串 . 如果匹配模式是字符串仅支持替换第一个匹配项 .

替换值可以是一个字符串 , 也可以是一个回调函数 .



**语法:**

```js
str.replace(regexp|substr, newSubStr|function)
```



- `regexp`

  正则表达式 , 匹配模式 .

- `substr`

  字符串 , 匹配模式 .

- `newSubStr`

  字符串 , 替换值 . 字符串可以插一些特殊的变量名 . 详情见文档 .

- `function`

  回调函数 , 替换值 . 回调可以接收到一些参数 , 详情见文档 .



**返回值:**

一个替换后新的字符串 .



**示例:**

*示例1*

```js
var reg = /[a-z]/g
var str = '123ab2325c78sss'
var result = str.replace(reg, '-')
console.log(result) // 123--2325-78---
```



*示例2*

```js
var reg = /[a-z]/g
var str = '123ab2325c78sss'
var result = str.replace(reg, function () {
    return '-'
})
console.log(result) // 123--2325-78---
```

