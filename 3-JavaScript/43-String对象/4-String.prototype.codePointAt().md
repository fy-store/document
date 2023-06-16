## String.prototype.codePointAt()

返回指定字符在Unicode中的位置 . 该方法支持解析超出 65535 的字符 .



**语法:**

```js
str.codePointAt(pos)
```



- `pos`

  这个字符串中需要转码的字符的位置



**返回值:**

如果给的位置的字符不存在 , 则返回 undefined



**示例:**

```js
var str = '😄'
var result = str.codePointAt(0)
console.log(result) // 128516
```

