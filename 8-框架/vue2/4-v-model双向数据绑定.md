## v-model

`v-model` 数据不仅能从实例对象中的数据流向页面，还可以从页面流向实例对象

`v-model` 只允许设置在表单类元素上 , 用于收集用户数据

`v-model:value=''` 可简写为 `v-model=''`



**示例:**

```html
<div id="app">
    <p>
        双向数据绑定: <input type="text" v-model:value="value1">
    </p>
    <p>
        简写双向数据绑定: <input type="text" v-model="value2">
    </p>
</div>
```



```js
const vm = new Vue({
    el: '#app',
    data() {
        return {
            value1: '',
            value2: ''
        }
    }
})
```





## 收集没有value值的表单

**收集单选框:**

需要为单选框指定一个 value 值 , 否则将收集将为 null

```html
<div id="app">
    性别:
    男:<input type="radio" name="sex" v-model="sex" value="male">
    女:<input type="radio" name="sex" v-model="sex" value="female">
</div>
```



```js
const vm = new Vue({
    el: '#app',
    data() {
        return {
            sex: ''
        }
    }
})
```



**收集多选框:**

收集多选框同样需要指定一个 value 值 , 并且收集数据储存方式必须为数组

否则将收集到 true/false , 并且会影响其他多选框

```html
<div id="app">
    爱好:
    游戏:<input type="checkbox" name="hobby" v-model="hobby" value="游戏">
    学习:<input type="checkbox" name="hobby" v-model="hobby" value="学习">
</div>
```



```js
const vm = new Vue({
    el: '#app',
    data() {
        return {
            hobby: []
        }
    }
})
```





## 常用表单修饰符

**number 数字:** 

按小数点砍断 , 转为数字类型

```html
<div id="app">
   验证码: <input type="text" v-model.number="code">
</div>
```



**lazy 惰性收集:**

失去焦点时收集 , 降低数据更新频率

```html
<div id="app">
   评价: <textarea v-model.lazy="val"></textarea>
</div>
```



**删除两端空格:**

```html
<div id="app">
   评价: <textarea v-model.trim="val"></textarea>
</div>
```

