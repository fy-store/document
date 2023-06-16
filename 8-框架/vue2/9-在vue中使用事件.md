## 在vue中使用事件

**事件的基本使用：**

1.使用 `v-on:xxx` 或 `@xxx` 绑定事件，其中 `xxx` 是事件名；

2.事件的回调需要配置在 `methods` 对象中，最终会挂载到 vm 上；

3.`methods` 中配置的函数，不能使用用箭头函数！否则 this 将不是 vm ；

4.``methods` 中配置的函数，都是被Vue所管理的函数，this 的指向是 vm 或 组件实例对象；



**示例:**

```html
<div id="app">
    <button v-on:click="func">v-on 点我弹窗-没有传参</button>
    <button v-on:click="func(123, $event)">v-on 点我弹窗-传参</button>
    <button @click="func">@xxx 点我弹窗-没有传参</button>
    <button @click="func(456, $event)">@xxx 点我弹窗-传参</button>
</div>
```



```js
const vm = new Vue({
    el: '#app',
    methods: {
        func(value, e) {
            alert('你好 vue')
            console.log(value, e);
        }
    }
})
```



**注意:**

不传参数: vue 将会把事件对象默认传递给函数的第一个参数

传递参数: vue 将会把你传递的参数依次传递给函数 , 若需要事件对象 , 可使用 `$event` 占位 , vue 将会把事件对象传递给占位参数的对应形参