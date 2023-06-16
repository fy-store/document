## Console 对象

[mdn文档](https://developer.mozilla.org/zh-CN/docs/Web/API/Console)

Console 对象是js中用于调试的对象 , 该对象上提供了很多的调试 api 方法



## console.log()

该方法用于在控制台中输出信息

```js
console.log(10)
```





## console.info()

该方法用于在控制台中输出信息 , 在谷歌浏览器中与 console.log() 一致

在 safari 中输出语句前面将带一个 ! 提示符

```js
console.info(10)
```





## console.dir()

该方法用于在控制台中输出信息 , 该方法可以展开某些特殊无法查看的对象

```js
console.dir(Function)
```





## console.table()

该方法用于在控制台中输出信息 , 输出的信息将按照表格的形式展示 , 很适合展示一些对象

```js
const person = {
    name: '小明',
    age: 20,
    set: 'male'
}
console.table(person)
```





## console.error()

该方法用于在控制台中输出错误信息 , 输出的信息将被标记错误 , 但是该方法不会抛出错误阻断程序运行

```js
console.error(10)
console.log(20)
```





## 更多待补充

请查看 mdn 文档