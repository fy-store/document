## Promise.any()

该方法接受一个具有 iterable 的数据, 如 Array , Set , Map 等 . 

其中如果有 Promise 将会被解析 . 非 Promise 将被包装成 Promise . 该方法返回一个 Promise . 

该方法会 *fulfilled* 兑现第一个成功的 Promise . 如果所有的都失败 , 该方法会 *rejected* 拒绝 , 拒绝原因将为一个 Error 对象 (AggregateError) . 



**示例:**

```js
const p1 = Promise.reject(1)
const p2 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(2)
    }, 2000)
})
const p3 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject(3)
    }, 3000)
})


const p = Promise.any([p1, p2, p3])
p.then((res) => {
    console.log(res) // 2
})
```

