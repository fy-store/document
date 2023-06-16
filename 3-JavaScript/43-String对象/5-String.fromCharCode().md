## String.fromCharCode()

静态方法 , 将指定的 UTF-16 代码单元序列创建成字符串 , 即将码点创建成字符串

该方法可以将多个字符的Unicode位置组合成一个字符串

组合字符串时对于大于 65535 的码点不进行有效性验证



**语法:**

```js
String.fromCharCode(num1[, ...[, numN]])
```



- `num`

  字符在Unicode中的位置, 范围介于 `0` 到 `65535`（`0xFFFF`）之间 . 大于 `0xFFFF` 的数字将被截断 . 不进行有效性检查 . 



**返回值:**

一个组合后的字符串 



**示例:**

*示例1*

```js
String.fromCharCode(65, 66, 67);   // "ABC"
```



*示例2*

```js
var str = '😄'
var str1 = str.charCodeAt(0)
var str2 = str.charCodeAt(1)
var result = String.fromCharCode(str1, str2)
console.log(result) // 😄
```

