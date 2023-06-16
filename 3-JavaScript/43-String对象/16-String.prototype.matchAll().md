## String.prototype.matchAll()

通过传入的正则表达式返回一个正则匹配结果的迭代器 .

需要注意的是这个方法传入的正则表达式必须使用 `g` 全局匹配 , 否则将抛出错误 .

该方法一般传入的规则为正则表达式 , 若是其他类型将会被包装成正则表达式 . 



**语法:**

```js
str.matchAll(regexp)
```



- `regexp`

  正则表达式



**返回值:**

一个迭代器（不可重用，结果耗尽需要再次调用方法的，要获取一个新的迭代器）



**示例:**

*示例1*

```js
var reg = /[a-z]/g
var str = '123a4a56'
var result = str.matchAll(reg)
console.log(result.next()) // {value: Array(1), done: false}
console.log(result.next()) // {value: Array(1), done: false}
console.log(result.next()) // {value: undefined, done: true}
```



*示例2*

使用 for of

```js
var reg = /[a-z]/g
var str = '123a4a56'
var result = str.matchAll(reg)

for (let i of result) {
    console.log(i);
}
// ['a', index: 3, input: '123a4a56', groups: undefined]
// ['a', index: 5, input: '123a4a56', groups: undefined]
```

