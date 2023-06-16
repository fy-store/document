## Promise.prototype.catch()

该方法用于统一处理 then 的错误 . 实际是 `Promise.prototype.then(undefined, onRejected)` 的简写 . 



**示例:**

```js
promise
    .then((res) => { })
    .then((res) => { })
    .then((res) => { })
    .catch((err) => {
        console.log('拒绝: ', err)
    })
```

