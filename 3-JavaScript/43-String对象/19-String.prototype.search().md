## String.prototype.search()

对该字符串指定查找一个指定字符串 , 如果存在则返回第一个出现的下标 , 如果不存在则返回 -1

查找模式一般为正则表达式 , 如果非正则表达式将会被隐式包装成正则表达式 .



**语法:**

```js
str.search(regexp)
```



- `regexp`

  正则表达式



**返回值:**

如果匹配成功，则返回正则表达式在字符串中首次匹配项的索引 , 不存在则返回 `-1`

所以该方法的正则表达式开不开去 `g` 全局都是一样的效果 .



**示例:**

```js
var reg = /[a-z]/
var str = '123ab2325c78sss'
var result = str.search(reg)
console.log(result) // 3
```

