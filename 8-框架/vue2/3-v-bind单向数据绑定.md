## v-bind

`v-bind` 是一个单向数据绑定 , 当数据发生变动时影响页面

指令中的语句可直接访问到 vue 实例对象中的值

`v-bind` 指令可以简写为 `:`



**示例:**

```html
<div id="app">
    <p>
        <a v-bind:href="url">点我去 {{url}}</a>
    </p>
    <p>
        <a :href="url" :data-url='url'>我是简写指令 {{url}}</a>
    </p>
</div>
```



```js
new Vue({
    el:'#app',
    data() {
        return {
            url: 'https://www.rgbcode.cn'
        }
    }
})
```

