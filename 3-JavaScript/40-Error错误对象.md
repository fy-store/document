## Error 错误对象

[mdn文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Error)

**错误类型:**

- EvalError : eval() 错误
- RangeError : 数值越界
- ReferenceError : 引用错误 , 非法或无效引用 `*`
- SyntaxError : 语法错误 `*`
- TypeError : 类型错误 , 操作数类型出错 `*`
- URIError : URI 处理函数使用不当
- AggregateError : 产生且需要报告的多个错误 , 如 Promise.any() 的错误



## 自定义错误类型

自定义错误后可以通过 `throw` 语句抛出错误

```js
try {
    console.log(a);
} catch (e) {
    const err = new Error('错误')
    throw err
}
```



**创建自定义具体类型的错误**

```js
try {
    console.log(a);
} catch (e) {
    const err = new SyntaxError('语法错误')
    throw err
}
```

