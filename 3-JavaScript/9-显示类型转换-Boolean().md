## Boolean()

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Boolean" target="_blank">MDN文档</a> 

使用 `Boolean()` 方法可以强制将一个数据转换成布尔值



**语法:**

```js
Boolean(data)
```

`data` 需要转换的数据



**示例:**

```js
Boolean('')// false (空串)
Boolean(0) // false
Boolean(undefined) // false
Boolean(null) // false
Boolean(false) // false
Boolean(NaN) // false
```



**转换规则:**

- 除以上 *6* 个值转换为布尔值为 `false` 外, 其他所有数据都为 `true`

