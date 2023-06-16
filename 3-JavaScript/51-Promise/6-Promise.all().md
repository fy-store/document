## Promise.all()

该方法接受一个具有 iterable 的数据, 如 Array , Set , Map 等 . 

其中如果有 Promise 将会被解析 . 非 Promise 将被包装成 Promise . 该方法返回一个 Promise . 

该方法只有当所有 Promise 解析完后状态才会确定 . 

该方法必须所有 Promise 都通过状态才会变更为 *fulfilled* , 如果有一个 *拒绝* , 则状态变更为 *rejected* , 并且 reject 的是第一个抛出的错误信息 . 



 **示例:**

```js
const p1 = 1
const p2 = 2
const p3 = Promise.resolve(3)
const p4 = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(4)
    }, 2000)
})


const p5 = Promise.all([p1, p2, p3, p4])
p5.then((res) => {
    console.log(res) // 2秒后输出 [1, 2, 3, 4]
})
```

