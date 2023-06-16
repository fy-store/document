## Number.prototype.toFixed()

对一个数采用四舍五入 , 使用定点表示法来格式化一个数值



**语法:**

```js
num.toFixed(digits)
```



- `digits`

  保留的小数个数, 取值范围为 0 - 20 , 实现环境可能支持更大范围 , 默认值为 0



**返回值:**

四舍五入后的字符串 .



**示例:**

```js
var num = 10
console.log(num.toFixed(2)) // '10.00'

var num = 10.123
console.log(num.toFixed(2)) // '10.12'
```

