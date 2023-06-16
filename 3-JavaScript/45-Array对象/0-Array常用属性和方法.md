## Array常用属性和方法

[mdn文档](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

通过 Array 构造函数能够创造一个数组 , 通过new调用和直接调用结果是一样的 .

当参数只为一个且是一个*正整数*时, 将作为数组的长度来创建数组, 内容为空 . 

其他类型, 或多个参数都将作为数组的每一项成员 . 

```js
var arr = new Array(5)
console.log(arr) // [空属性 × 5]
```

