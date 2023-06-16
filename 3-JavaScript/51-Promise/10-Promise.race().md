## Promise.race()

该方法接受一个具有 iterable 的数据, 如 Array , Set , Map 等 . 

其中如果有 Promise 将会被解析 . 非 Promise 将被包装成 Promise . 该方法返回一个 Promise .

一旦迭代器中的某个 promise 解决或拒绝，返回的 promise 就会解决或拒绝 . 



**示例:**

```js
const p1 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(1)
    }, 3000)
})
const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject(2)
    }, 2000)
})

const p = Promise.race([p1, p2])
p.then(
    res => {
        console.log(res)
    },
    err => {
        console.log('err', err) // 输出
    }
)
```

