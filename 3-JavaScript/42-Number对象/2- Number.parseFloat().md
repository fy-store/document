## Number.parseFloat()

`Number.parseFloat()` 方法可以把一个字符串解析成浮点数, 该方法与全局的 `parseFloat()` 函数相同

如果传入的参数不是字符串, 将会被转为字符串 , 两端的空白将会被忽略 , 最终返回一个浮点数





**语法:**

```js
parseFloat(string)
```



- `string`  

  需要被解析成为浮点数的值



```js
Number.parseFloat('     1.1     ') // 1.1
Number.parseFloat(1.1) // 1.1
Number.parseFloat('1.1.2') // 1.1
Number.parseFloat('1.1abc') // 1.1
Number.parseFloat(Infinity) // Infinity
```



**返回值:**

转换成功返回一个浮点数

转换失败通常返回 `NaN`

如果是 `Infinity` 则返回 `Infinity` 

如果是 `-Infinity` 则返回 `-Infinity`

如果转换 ` BigInt` 将会精度丢失 , 末尾 n 会被遗弃