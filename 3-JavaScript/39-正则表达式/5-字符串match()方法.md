## 字符串 `match()` 方法

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/match"
        target="_blank">MDN文档</a> 

**String.prototype.match()**

**`match()`** 方法检索返回一个字符串匹配正则表达式的结果



**语法:**

```js
str.match(regexp)
```



**参数:**

`regexp`

一个正则表达式对象或者任何具有 Symbol.match 方法的对象

如果 `regexp` 不是 `RegExp` 对象并且对象上无 `Symbol.match` 方法，则会使用 `new RegExp(regexp)` 将其隐式地转换为 `regexp`

如果你没有给出任何参数并直接使用 `match()` 方法，你将会得到一个包含空字符串的数组：`[""]`，因为这等价于 `match(/(?:)/)`



**返回值:**

- 如果使用 `g` 标志，则将返回与完整正则表达式匹配的所有结果，但不会返回捕获组。
- 如果未使用 `g` 标志，则仅返回第一个完整匹配及其相关的捕获组（`Array`）。在这种情况下，返回的项目将具有如下所述的其他属性。
  - `groups` : 一个命名捕获组对象，其键是捕获组名称，值是捕获组，如果未定义命名捕获组，则为 `undefined` 。有关详细信息，请参阅组和范围。
  - `index`: 匹配的结果的开始位置
  - `input`: 搜索的字符串。



**描述:**

如果正则表达式不包含 `g` 标志，str.match() 将返回与 RegExp.exec(). 相同的结果(匹配不到返回 null)



**示例:**

```js
const reg = /[a-z]/;
const str = 'defabc123abc';
let result1 = str.match(reg);
console.log(result1); // ['d', index: 0, input: 'defabc123abc', groups: undefined]
```



**全局匹配:**

包含 `g`

```js
const reg = /[a-z]/g;
const str = 'defabc123abc';
let result1 = str.match(reg);
console.log(result1); // ['d', 'e', 'f', 'a', 'b', 'c', 'a', 'b', 'c']
```





**关于使用:**

- 如果你需要知道一个字符串是否与一个正则表达式匹配 [`RegExp`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp) ，可使用 [`RegExp.test()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/test) 。
- 如果你只是需要第一个匹配结果，你也可以使用 [`RegExp.exec()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) 。
- 如果你想要获得捕获组，并且设置了全局标志，你需要用 [`RegExp.exec()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/RegExp/exec) 或者 [`String.prototype.matchAll()`](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/String/matchAll)