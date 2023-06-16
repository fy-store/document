## 正则表达式 `exec()` 方法 

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec"
        target="_blank">MDN文档</a> 

**RegExp.prototype.exec()**

**`exec()`** 方法在一个指定字符串中执行一个搜索匹配。返回一个结果数组或 `null`



**语法:**

```js
reg.exec(str)
```



**示例:**

```js
const reg = /abc/;
const str = 'defabc123abc';
let result1 = reg.exec(str);
let result2 = reg.exec(str);
console.log(result1); // ['abc', index: 3, input: 'defabc123abc', groups: undefined]
console.log(result2); // ['abc', index: 3, input: 'defabc123abc', groups: undefined]
```



**返回值:**

如果匹配失败，``exec()`` 方法返回 `null` ，并将正则表达式的 `lastIndex` 重置为 0

如果匹配成功，`exec()` 方法返回一个数组，并更新正则表达式对象的 `lastIndex` 属性。完全匹配成功的文本将作为返回数组的第一项，从第二项起，后续每项都对应一个匹配的捕获组。数组还具有以下额外的属性：

`index`

匹配到的字符位于原始字符串的基于 0 的索引值



`input`

匹配的原始字符串



`groups`

一个命名捕获组对象，其键是名称，值是捕获组。若没有定义命名捕获组，则 `groups` 的值为 `undefined` 。参阅捕获组以了解更多信息



`indices` [可选]

此属性仅在设置了 `d` 标志位时存在。它是一个数组，其中每一个元素表示一个子字符串的边界。每个子字符串匹配本身就是一个数组，其中第一个元素表示起始索引，第二个元素表示结束索引





## 当使用全局匹配时

`index` 属性将会接力下去

```js
const reg = /abc/g;
const str = 'defabc123abc';
let result1 = reg.exec(str);
let result2 = reg.exec(str);
console.log(result1); // ['abc', index: 3, input: 'defabc123abc', groups: undefined]
console.log(result2); // ['abc', index: 9, input: 'defabc123abc', groups: undefined]
```





## 关于使用

`exec()` 是正则表达式的原始方法。许多其它的正则表达式方法会在内部调用 `exec()`——包括一些字符串方法也会调用 `exec()`，如 [`@@replace`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/@@replace)。虽然 `exec()` 本身非常强大而又有效，但它通常不能最清楚地表示调用的目的。

- 如果你只是为了判断是否匹配，请使用 [`RegExp.prototype.test()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test) 方法代替。
- 如果你只是为了找出所有匹配正则表达式的字符串而又不关心捕获组，请使用 [`String.prototype.match()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match) 方法代替。此外，[`String.prototype.matchAll()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll) 允许你对匹配项进行迭代，这有助于简化匹配字符串的多个部分（带有匹配组）。
- 如果你只是为了查找在字符串中匹配的索引，请使用 [`String.prototype.search()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/search) 方法代替。