## String()

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String" target="_blank">MDN文档</a> 

使用 `String()` 方法可以强制将一个数据转换成字符串



**语法:**

```js
String(data)
```

`data` 需要转换的数据



**示例:**

```js
String(123) // '123'
String(true) // 'true'
String([1, 2, 3]) // '1,2,3'
String({name: 'abc'}) // '[object Object]'
String(0b11) // '3'
String(0o66) // '54'
String(0x88) // '136'
String('0b11') // '0b11'
String(undefined) // 'undefined'
String(null) // 'null'
```



**转换规则:**

- 将数据强制转换为字符串

- 将对应进制数字转换为 10进制字符串





##  常见转义字符

- `\n` 换行 
- `\t` 制表 
- `\b` 退格 
- `\r` 回车 
- `\f` 换页 
- `\\` 反斜杠
- `\'` 单引号

- `\"` 双引号

- *\\`* 反引号

