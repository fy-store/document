## Number.parseInt()

`Number.parseInt()` 方法依据指定基数，解析字符串并返回一个10进制整数

这个方法和全局的 parseInt() 函数具有一样的函数功能

该方法也可用于对小数取整 , 正负数取整都是向 0 取整 , 正数和 Math.floor() 一样 , 负数则有差异



**语法:**

```js
Number.parseInt(string [, radix])
```



- `string`  

  要被解析的值 , 如果参数不是一个字符串，则将其强制转化为字符串 . 字符串开头的空白符将会被忽略



- `radix` 

  指定第一个参数的进制数 , 范围为 2 到 36 的整数，表示进制的基数 . 如果超出这个范围，将返回 NaN . 

  假如 radix 未指定或者为 0，除非数字以 0x 或 0X 开头，否则将被假定为 10 进制



**返回值:**

如果解析成功将返回一个 10 进制整数

如果解析失败将返回 NaN



**示例:**

```js
var num = Number.parseInt('b', 16)
console.log(num); // 11
```

