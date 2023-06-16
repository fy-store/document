## Vue.set()

当你希望给Vue实例对象中的数据添加一个响应式数据时可使用 `Vue.set()` 方法

在实例对象内部添加响应式数据时可使用 `$set()` 方法



**注意:**

不能给 `vm` 或 `vm` 的根数据对象 添加属性！！！



**小贴士:**

对象中后追加的属性，Vue默认不做响应式处理

数组使用下标修改/添加的数据默认不做响应式出来



**语法:** `this.$set(target, 'attribute|index', data)`



**参数:**

`target` 添加数据数据的目标

`attribute` 添加的属性名

`data` 添加的属性值



**示例:**

```html
<div id="app">
    <div>小明的性别是: {{person['小明'].sex}} , 年龄是: {{person['小明'].age}}</div>
    <input type="text" v-model="age"> <button @click="add('小明')">为小明添加年龄</button>
</div>
```



```js
const vm = new Vue({
    el: '#app',
    data() {
        return {
            age: null,
            person: {
                '小明': {
                    sex: '男'
                }
            }
        }
    },
    methods: {
        add(val) {
            this.$set(this.person[val], 'age', this.age)
        }
    }
})
```

