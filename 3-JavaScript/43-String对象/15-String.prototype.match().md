## String.prototype.match()

该方法通过传入的正则表达式检索出对应的正则匹配结果

该方法一般传入的规则为正则表达式 , 若是其他类型将会被包装成正则表达式



**语法:**

```js
str.match(regexp)
```



- `regexp`

  正则表达式



**返回值:**

正则表达式的匹配结果 , 未匹配到则返回 null



**示例:**

*示例1*

```js
var reg = /[a-z]/
var str = '123a4a56'
var result = str.match(reg)
console.log(result); // ['a', index: 3, input: '123a4a56', groups: undefined]
```



*示例2*

使用全局匹配 , 获得捕获组

```js
var reg = /[a-z]/g
var str = '123a4a56'
var result = str.match(reg)
console.log(result); // ['a', 'a']
```

