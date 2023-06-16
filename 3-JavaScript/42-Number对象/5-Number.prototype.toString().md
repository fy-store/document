## Number.prototype.toString()

将调用者作为十进制 , 参数作为指定进制数 , 返回指定进制数字符串

该方法也通常被用作为数字类型转字符串类型的方法 .



**语法:**

```js
numObj.toString([radix])
```



- `radix`

  指定转换目标的进制数 , 范围为 2 - 36 , 默认值为 10 .



**返回值:**

数值转换后的字符串



**示例:**

```js
var num = 10
console.log(num.toString(2)) // '1010'
```

