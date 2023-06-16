## vue 中的this指向

vue 实例后会将所管理的普通函数的 `this` 指向该 vue 实例



**示例:**

```js
const vm = new Vue({
    el: '#app',
    data() {
        console.log(this)
        return {
            func() {
				console.log(this)
            }
        }
    }
})
```



**注意:**

所以被 vue 所管理的函数不建议书写成箭头函数