## String.prototype.charCodeAt()

返回指定字符在Unicode中的位置 . 

返回 `0` 到 `65535` 之间的整数，表示给定索引处的 UTF-16 代码单元

这里的 0 - 65535 , 即 2的16次方 , 就是说它只能解析单个码元的字符 . 如果是多个码元组成的字符(码点)它只能解析第一个码元 . 

如果想要整个码点的值，可以使用 `codePointAt()`



**语法:**

```js
str.charCodeAt(index)
```



- `index`

  一个大于等于 `0`，小于字符串长度的整数 , 如果不是一个数值，则默认为 `0` 

​			

**返回值:**

指定字符的 Unicode 位置 , index 如果超出范围将返回 NaN



**示例:**

```js
var str = 'abc'
var result = str.charCodeAt(1)
console.log(result) // 98
```

