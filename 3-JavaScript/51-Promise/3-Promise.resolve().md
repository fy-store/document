## Promise.resolve()

该方法用于快速返回一个 Promise , 如果传入的是普通数据, 则返回的是一个 *fulfilled* 状态的promise (then执行过程没报错就) .

如果传入的是一个 Promise , 那么将返回这个 Promise , 具体 *fulfilled* 还是 *rejected* 看这个传入的 Promise . 

如果传入的 Promise 跟随着 *thenable* (调用了then) , 那么最终状态看 *then* 最终的结果 . 



**示例传入的是普通数据:**

```js
const p = Promise.resolve(10)
p.then(res => {
    console.log('成功: ', res)
})
```



**示例传入的是Promise:**

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(10)
    }, 2000)
}).then(res => {
    throw '拒绝'
})

const p2 = Promise.resolve(p1)
p2.then(res => {
    console.log('成功', res)
}).catch(err => {
    console.log(err) // 错误将在这里被处理, 不会被抛出
})
```

