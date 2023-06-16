## Promise.reject()

该方法快速创建一个拒绝状态的 Promise . 

传入的数据不管是普通数据还是 Promise 都会被作为拒绝原因 . Promise 不会像 Promise.resolve() 那样做特殊处理 . 



**示例:**

```js
const p2 = Promise.reject('拒绝')
p2.then(res => {
    console.log('成功', res)
}).catch(err => {
    console.log(err) // 输出 '拒绝'
})
```

