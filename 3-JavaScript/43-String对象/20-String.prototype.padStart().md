## String.prototype.padStart()

该方法会用一个字符串填充当前字符串 , 将该字符串填充至指定长度 , 在开头开始填充 (如果有需要填充字符串将会重复)



**语法:**

```js
str.padStart(targetLength [, padString])
```



- `targetLength`

  当前字符串需要填充到的目标长度 , 如果这个数值小于当前字符串的长度，则返回当前字符串本身

- `padString` [可选]

  填充的字符串 , 此参数如果缺省值将为 " " (一个空格), 填充后的字符串如果超过目标长度, 那么"填充字符串"将会被截断 , 只保留左侧 .



**返回值:**

一个填充后新的字符串 .



**示例:**

```js
var str = 'abc'
var result = str.padStart(5, 'def')
console.log(result) // deabc
console.log(result.length) 5
```

