## 正则表达式 `test()` 方法

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test"
        target="_blank">MDN文档</a> 

**RegExp.prototype.test()**

**`test()`** 方法执行一个检索，用来查看正则表达式与指定的字符串是否匹配。返回 `true` 或 `false`。



**语法:**

```js
reg.test(str)
```



**示例:**

如果正则表达式与指定的字符串匹配，返回 `true` ；否则`false` 

```js
const reg = /abc/;
const str = 'defabc123';
let result = reg.test(str)
console.log(result); // true
```





## 当设置全局标志的正则使用 `test()`

如果正则表达式设置了全局标志，`test()` 的执行会改变正则表达式 `lastIndex` 属性。连续的执行 `test()` 方法，后续的执行将会从 `lastIndex` 处开始匹配字符串 .



**示例:**

```js
const reg = /abc/g;
        const str = 'defabc123';
        let result1 = reg.test(str);
        let result2 = reg.test(str);
        console.log(result1); // true
        console.log(result2); // false
```

