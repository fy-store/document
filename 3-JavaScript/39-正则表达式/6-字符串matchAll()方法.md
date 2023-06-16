## 字符串的 `matchAll()` 方法

[mdn文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll)

**String.prototype.matchAll()**

**`matchAll()`** 方法返回一个包含所有匹配正则表达式的结果及分组捕获组的迭代器。

该方法所使用的正则表达式必须为全局匹配 , 即添加了 `g` 标志 , 否则将报错 , 返回的是一个迭代器 .



**语法:**

```js
str.matchAll(regexp)
```



**参数:**

`regexp`

正则表达式对象。如果所传参数不是一个正则表达式对象，则会隐式地使用 new RegExp(obj) 将其转换为一个 RegExp , 即可以为字符串 , 内部会隐式转换为正则表达式对象 .



**返回值:**

一个迭代器



**示例1:**

```js
const reg = /[a-z]/g;
const str = 'defabc123abc';
let result = str.matchAll(reg);
console.log(result.next()); 
console.log(result.next()); 
console.log(result.next()); 
```



**示例2:**

```js
const reg = /[a-z]/g;
const str = 'defabc123abc';
let result = str.matchAll(reg);
for (let i of result) {
    console.log(i);
}
```





**本章结语:**

在 `matchAll` 出现之前，通过在循环中调用 `regexp.exec()` 来获取所有匹配项信息（regexp 需使用 `/g` 标志）