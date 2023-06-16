## then 方法

根据Promise A+ 规范规定 , 只要一个函数或对象上具有一个 *then* 方法, 那么它就是一个 Promise .

一个 *then* 方法将会接受两个函数 , 第一个函数为 Promise 成功的回调 , 第二个函数为 Promise 失败的回调 . 

函数中可以接受 Promise 更改状态传递过来的数据 . 

回调函数可以置空 . 但是若发生错误 , *then* 方法没有一个处理 *rejected* 的函数时将抛出错误 . 



## then 方法链式调用

每一个 then 方法都会返回一个 Promise . 

在链式调用中 , then 处理函数的返回值将作为下一个 then 的数据(会被包装成Promise) .

then 方法传递的 "回调" 若不是一个函数 , 将被忽略 , 上一个 Promise 的返回状态将被 "透传" . 

then 方法处理函数中只要不报错即为成功 . 需要注意的是 then 方法中捕获不了异步错误 . 





## 示例

*模拟请求*

```js
const promise = new Promise((resolve, reject) => {
    setTimeout(() => {
        resolve(10)
    }, 2000)
})

promise.then(
    (res) => {
        console.log(res)
    },
    (err) => {
        console.log('拒绝: ', err)
    }
)
```

