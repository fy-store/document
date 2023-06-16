## call 和 apply

**作用：**

改变this指向

改变运行时this指向



**区别：**

传参列表的形式不同

call若需要传递参数直接在后续传就可以, apply参数则需传递一个数组



`call` 和 `apply` 改变函数运行时的 `this` 指向



**call()**

`func.call(thisObject [, 参数1, 参数2 ...])`

```js
var obj = {
    name: '小白'
}

function test(a, b, c) {
    console.log(this)
    console.log(a, b, c)
}

test.call(obj, 'aaa', 'bbb')
```



**apply()**

`func.apply(thisObject [,[参数1, 参数2 ...]])`

```js
var obj = {
    name: '小白'
}

function test(a, b, c) {
    console.log(this)
    console.log(a, b, c)
}

test.apply(obj, ['aaa', 'bbb', 'ccc'])
```





## bind

bind 用于绑定一个函数的 this 指向, 只绑定但不执行, 返回一个绑定后的函数

普通函数和箭头函数都可以调用 `bind()` 但是箭头函数使用 `bind()` 是无效的

`func.bind(thisObject [, 参数1, 参数2 ...])`

在使用 `bind()` 的过程中同样可传递参数, 最终执行时参数将按照先后顺序依次传入执行的函数中 

```js
var obj = {
    name: '小白'
}

function test(a, b, c) {
    console.log(this)
    console.log(a, b, c)
}

var newTest = test.bind(obj, 'aaa', 'bbb')
newTest('ccc') 
// {name: '小白'}
// aaa bbb ccc
```

