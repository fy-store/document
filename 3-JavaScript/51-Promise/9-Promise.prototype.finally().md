## Promise.prototype.finally()

该方法无论 Promise 是 *fulfilled* 还是 *rejected* 都会执行一次 . 该方法不接受参数 . 



**示例:**

```js
const p = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject('拒绝')
    }, 2000)
})

p.catch(err => {})
.finally(() => {
    console.log('执行 finally') // 输出
})
```

