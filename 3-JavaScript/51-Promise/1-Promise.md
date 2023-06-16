## Promise

Promise 是官方推出的标准异步解决方案 . 

创建 Promise ( new Promise ) 执行时是同步的 , then 调用是异步的 .

then 的运行将被放入 *微队列* 中 . 



**创建一个Promise**

*语法*

```js
const p = new Promise(executor)
```



- `executor` 

  执行器函数, 接受两个参数, 分别是 `resolut` 和 `reject` , 它们两个都是函数, 调用时都可传递一个参数 . 

  调用 *resolut* 表示 Promise 成功 , Promise 状态将从 *pending* 变成 *fulfilled* 

  调用 *reject* 表示 Promise 失败(被拒绝) , Promise 状态将从 *pending* 变成 *rejected*





## Promise 的三种状态

一个 `Promise` 必然处于以下几种状态之一：

- *待定（pending）*：初始状态，既没有被兑现，也没有被拒绝。
- *已兑现（fulfilled）*：意味着操作成功完成。
- *已拒绝（rejected）*：意味着操作失败。



一旦状态从 *pending* 变更为其他状态, 那么它的状态就已经确定, 后续不可改变 . 