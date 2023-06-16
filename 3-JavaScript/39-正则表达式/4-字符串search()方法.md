## 字符串 `search()` 方法

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/search"
        target="_blank">MDN文档</a> 

**String.prototype.search()**

`search()` 方法执行正则表达式和 `String` 对象之间的一个搜索匹配



**语法:**

```js
str.search(regexp)
```



**参数:**

`regexp`

一个 `正则表达式(regular expression)` 对象 . 如果传入一个非正则表达式对象 `regexp`，则会使用 `new RegExp(regexp)` 隐式地将其转换为正则表达式对象 .



**返回值:**

如果匹配成功，则 `search()` 返回正则表达式在字符串中首次匹配项的索引; 否则，返回 `-1` .



**示例:**

```js
const reg = /abc/g;
const str = 'defabc123abc';
let result = str.search(reg);
console.log(result); // 3
```



**关于使用:**

当你想要知道字符串中是否存在某个模式（pattern）时可使用 `search()`，类似于正则表达式的 `test()` 方法。