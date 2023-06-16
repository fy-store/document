## 使用 vue

**创建 vue 实例:**

```html
<div id="app">{{name}}</div>
```



```js
const vm = new vue({
    el:'#app',
    data() {
        return {
            name: 'xxx',
            age: 19
        }
    }
})
```



- `{{}}` 被称为插值语法 , 可以直接访问到 vue 实例对象中的数据 , 例如 `data` 中的数据 , 插件语法中书写的值必须为 js 表达式
- vue 实例对象
  - `el` 绑定一个容器 , 将这个容器交给 vue 控制
  - `data` 数据 , 该属性可以直接使用一个对象 , 但通常不建议 , 因为在组件中必须使用函数以保证每个组件的作用域 , 放在组件冲突 , 所有通常 `data` 属性我们会书写成一个 `函数` , `data` 中的数据是响应式的 



**关闭生产提示:**

```js
Vue.config.productionTip = false
```

