## Number()

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Number" target="_blank">MDN文档</a> 

使用 `Number()` 方法可以强制将一个数据转换成数字类型



**语法:**

```js
Number(data)
```

`data` 需要转换的数据



**示例:**

```js
Number('  123   ') // 123
Number('0000123') // 123
Number(01) // 1
Number(0O22) // 18
Number(0x33) // 51
Number('0x33') // 51
Number('0b11') // 3
Number('123abc11') // NaN
Number('123.123') // 123.123
Number('123.123.123') // NaN
```





**转换规则:**

- 忽略左右空白字符
- 忽略左边所有 *0* 字符

- 其他进制将会被转换为 10进制数字

- 转换失败将返回 NaN
  - 需注意 NaN 属于数字类型
  - 即: `typeof NaN` // 'number'



## js中的进制表示

- 正常书写为 10进制
- `0x` 开头为 16进制
- `0o` 开头为 8进制
- `0b` 开头为 2进制

进制中的字符不区分大小写

0进制 和 1进制 无意义

最大进制表示为 36进制, 即 0 - 9 加上 a - z  , 10个数字 + 26个字符 === 36个表示字符





## 其他

`NaN` 属于数字类型, 表示非数 (无法用数字进行表示)

`NaN` 不等于任何数, 包括 `NaN` 

当一个数计算不尽或数值溢出时将返回 `Infinity` 或 `-Infinity`

`Infinity` 属于数字类型, 表示无穷

js中 +0 等于 -0

*示例:*

```js
1 / 0 // Infinity
-1 / 0 // -Infinity
+0 === -0 // true
```

