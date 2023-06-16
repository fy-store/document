## Promise.allSettled()

该方法接受一个具有 iterable 的数据, 如 Array , Set , Map 等 . 

其中如果有 Promise 将会被解析 . 非 Promise 将被包装成 Promise . 该方法返回一个 Promise . 

当所有 Promise 的状态都敲定后 , 返回的 Promise 将被兑现, 状态为 *fulfilled* . 

返回的参数为一个描述 Promise 的对象数组 . 



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
const p5 = new Promise((resolve, reject) => {
    setTimeout(() => {
        reject(5)
    }, 3000)
})


const p = Promise.allSettled([p1, p2, p3, p4, p5])
p.then((res) => {
    console.log(res) 
    // 返回
    [
        {status: 'fulfilled', value: 1}
        {status: 'fulfilled', value: 2}
        {status: 'fulfilled', value: 3}
		{status: 'fulfilled', value: 4}
		{status: 'rejected', value: 5}
    ]
})
```

