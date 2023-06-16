## vue 绑定容器的两种写法

(1).new Vue 时候配置 `el` 属性。

(2).先创建 Vue 实例，随后再通过 `vm.$mount()` 方法指定 `el` 的值。



**示例:**

```html
<div id="app">
</div>
```



**第一种:**

```js
new Vue({
    el: '#app'
})
```



**第二种:**

```js
const vm = new Vue({
    el: '#app'
})
vm.$mount('#app')
```

