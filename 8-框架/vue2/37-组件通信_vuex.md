## Vuex

**概念:**

在Vue中实现集中式状态（数据）管理的一个Vue插件，对vue应用中多个组件的共享状态进行集中式的管理（读/写），也是一种组件间通信的方式，且适用于任意组件间通信。



**何时使用？**

多个组件需要共享数据时

多个组件依赖于同一种状态

来自不同组件的行为需要变更同一状态



**vuex示图:**

![vuex](./images/vuex.png)



**安装vuex:**

vue2对应vuex@3 vue3对应vuex@4

```npm
npm i vuex@3
or
yarn add vuex@3
```



**搭建vuex环境:**

创建文件：`src/store/index.js`

```js
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

export default new Vuex.Store({
    state: { // 状态(数据)
        count: 0
    },
    mutations: { // 用于变更状态(操作数据)
        increment(state) {
            state.count++;
        }
    }
});
```



**main.js:**

在 ```main.js``` 中创建vm时传入 ```store``` 的 vuex 配置项 , 文件名 index 可省略

```js
import Vue from 'vue'
import App from './App.vue'
import store from './store'

Vue.config.productionTip = false

new Vue({
  el: '#app',
  render: h => h(App),
  store // 从根组件中注入 vuex , 使每个组件都可使用 $store
})
```







## 基础应用

**vuex中:**

`src/store/index.js`

```js
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

// 用于响应组件触发状态
const actions = {
    increment(context, value) {
        // context 上下文 , 是一个 mini store
        // value 传递过来的数据
        context.commit('INCREMENT', value); // 触发 mutations 中的状态
    }
}

// 真正用于变更状态(操作数据)
const mutations = {
    // 此处key一般命名为大写
    INCREMENT(state, value) {
        // state 真正的状态(数据)
        // value 传递过来的值
        state.count++;
        console.log(state, value);
    }
}

// 类似于计算属性, 用于加工 state 中的状态(数据)
// 如果逻辑复杂又想组件复用, 可以使用 getters
const getters = {
    bigCount(state) {
        return state.count * 10
    }
}

export default new Vuex.Store({
    actions,
    mutations,
    state,
    getters
});
```



**main.js:**

```js
import Vue from 'vue'
import App from './App.vue'
import store from './store'

Vue.config.productionTip = false

new Vue({
  el: '#app',
  render: h => h(App),
  store // 从根组件中注入 vuex , 使每个组件都可使用 $store
})
```



**组件中:**

```vue
<template>
  <div class="count">
    <h2>计数:</h2>
    <div>
      {{ $store.state.count }} <!-- 读取vuex中的数据 count -->
    </div>
    <div>
      放大10倍后: {{ $store.getters.bigCount }} <!-- 使用getters -->
    </div>
    <button @click="increment">增加</button>
  </div>
</template>

<script>
export default {
  name: "TestVue",
  methods: {
    increment() {
      this.$store.dispatch("increment"); // 触发 increment 状态, 第二个参数为传递的数据
      // this.$store.commit("INCREMENT"); // 第二个参数为传递的数据
      // 如果没有什么业务逻辑需要处理此处可直接调用 commit
      // dispatch 一般在此处发送 ajax 等
    },
  },
};
</script>

<style lang="sass" scoped>
.count
  margin-top: 30px
  margin-left: 30px
</style>
```





## 四个map方法的使用

用于简写代码



### mapState 和 mapGetters

**vuex:**

```js
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

// 用于响应组件触发状态
const actions = {
    increment(context, value) {
        context.commit('INCREMENT', value);
    }
}

// 用于变更状态(操作数据)
const mutations = {
    INCREMENT(state) {
        state.count++;
    }
}

// 存储状态(数据)
const state = {
    count: 0,
    hello: 'hello vue',
}

// 类似于计算属性 , 用于加工 state 中的状态(数据)
const getters = {
    bigCount(state) {
        return state.count * 10
    }
}

export default new Vuex.Store({
    actions,
    mutations,
    state,
    getters
});
```



**使用vue计算属性简化插值语法:**

组件中

```vue
<template>
  <div class="count">
    <h2>计数:</h2>
    <div>
      {{ count }}
    </div>
    <div>放大10倍后: {{ bigCount }}</div>
    <div>你好:{{ hello }}</div>
    <button @click="increment">增加</button>
  </div>
</template>

<script>
export default {
  name: "TestVue",
  methods: {
    increment() {
      this.$store.dispatch("increment");
    },
  },
  computed: {
    // 使用计算属性简化插值语法
    // 简化读取 state
    count() {
      return this.$store.state.count;
    },
    hello() {
      return this.$store.state.hello;
    },
    // 简化读取 getters
    bigCount() {
      return this.$store.getters.bigCount;
    },
  },
};
</script>

<style lang="sass" scoped>
.count
  margin-top: 30px
  margin-left: 30px

  div
    padding: 5px 0
</style>
```



**使用vuex提供的map简化计算属性:**

组件中

```vue
<template>
  <div class="count">
    <h2>计数:</h2>
    <div>
      {{ count }}
    </div>
    <div>放大10倍后: {{ bigCount }}</div>
    <div>你好:{{ hello }}</div>
    <button @click="increment">增加</button>
  </div>
</template>

<script>
// 导入 vuex 提供的 map 方法
import { mapState, mapGetters } from "vuex";

export default {
  name: "TestVue",
  methods: {
    increment() {
      this.$store.dispatch("increment");
    },
  },
  computed: {
    // 使用vuex提供的map简化计算属性
    // 对象形式简化读取 state
    // ...mapState({ count: "count", hello: "hello" }),
    // 数组形式简化读取 state
    ...mapState(["count", "hello"]),

    // 对象形式简化读取 getters
    // ...mapGetters({ bigCount: "bigCount" }),
    // 数组形式简化读取 getters
    ...mapGetters(["bigCount"]),
  },
};
</script>

<style lang="sass" scoped>
.count
  margin-top: 30px
  margin-left: 30px

  div
    padding: 5px 0
</style>
```





### mapActions 和 mapMutations

mapActions 用于简写 dispatch

mapMutations 用于简写 commit



**vuex:**

```js
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);

// 用于响应组件触发状态
const actions = {
    increment(context, value) {
        context.commit('INCREMENT', value);
    }
}

// 用于变更状态(操作数据)
const mutations = {
    INCREMENT(state, value) {
        state.count += value;
    }
}

// 存储状态(数据)
const state = {
    count: 0,
    hello: 'hello vue',
}

// 类似于计算属性 , 用于加工 state 中的状态(数据)
const getters = {
    bigCount(state) {
        return state.count * 10
    }
}

export default new Vuex.Store({
    actions,
    mutations,
    state,
    getters
});
```



**使用原始vue触发状态:**

组件中

```vue
<template>
  <div class="count">
    <h2>计数:</h2>
    <div>
      {{ count }}
    </div>
    <div>放大10倍后: {{ bigCount }}</div>
    <div>你好:{{ hello }}</div>
    <input type="text" v-model.number="num" />
    <button @click="increment">增加</button>
  </div>
</template>

<script>
// 导入 vuex 提供的 map 方法
import { mapState, mapGetters } from "vuex";

export default {
  name: "TestVue",
  data() {
    return {
      num: 1,
    };
  },
  methods: {
    // 使用原始vue触发状态
    increment() {
      this.$store.dispatch("increment", this.num);
    },
  },
  computed: {
    // 使用vuex提供的map简化计算属性
    ...mapState(["count", "hello"]),
    ...mapGetters(["bigCount"]),
  },
};
</script>

<style lang="sass" scoped>
.count
  margin-top: 30px
  margin-left: 30px

  div
    padding: 5px 0
</style>

```



**使用vuex提供的map进行简写:**

mapActions 用于简写 dispatch

mapMutations 用于简写 commit



组件中

```vue
<template>
  <div class="count">
    <h2>计数:</h2>
    <div>
      {{ count }}
    </div>
    <div>放大10倍后: {{ bigCount }}</div>
    <div>你好:{{ hello }}</div>
    <input type="text" v-model.number="num" />
    <!-- --------------------------------------------- -->
    <!-- <button @click="increment">增加</button> -->
    <!-- 
        mapActions 和 mapMutations 简写不能直接传递数据,
        所以当需要传递数据时需要在此处事先传递数据
    -->
    <button @click="increment(num)">增加</button>
    <!-- --------------------------------------------- -->
  </div>
</template>

<script>
// 导入 vuex 提供的 map 方法
import { mapState, mapGetters, mapActions, mapMutations } from "vuex";

export default {
  name: "TestVue",
  data() {
    return {
      num: 1,
    };
  },
  methods: {
    // 简写 dispatch
    // 对象简写
    // ...mapActions({ increment: "increment" }),
    // 数组简写
    ...mapActions(["increment"]),
    //
    // 原始vue写法
    // increment() {
    //   this.$store.dispatch("increment", this.num);
    // },
    //
    // -------------------------------------------------------
    //
    // 简写 commit
    // 对象简写
    // ...mapMutations({ increment: "INCREMENT" }),
    // 数组简写
    // ...mapMutations(["INCREMENT"]), 此处需要与函数调用命名保持一致
    //
    // 原始vue写法
    // increment() {
    //   this.$store.commit("INCREMENT", this.num);
    // },
  },
  computed: {
    // 使用vuex提供的map简化计算属性
    ...mapState(["count", "hello"]),
    ...mapGetters(["bigCount"]),
  },
};
</script>

<style lang="sass" scoped>
.count
  margin-top: 30px
  margin-left: 30px

  div
    padding: 5px 0
</style>
```





## 模块化和命名空间

**目的：**

让代码更好维护，让多种数据分类更加明确。



**示例:**

vuex  `src/store/index.js`

```js
import Vue from 'vue';
import Vuex from 'vuex';

Vue.use(Vuex);


// const test = {
//     namespaced: true, //开启命名空间
//     state: {}, // 存储状态(数据)
//     mutations: {}, // 用于变更状态(操作数据)
//     actions: {}, // 用于响应组件触发状态
//     getters: {} //  类似于计算属性 , 用于加工 state 中的状态(数据) , 处理复杂逻辑
// }

const test1 = {
    namespaced: true, //开启命名空间
    state: {
        count: 0,
        hello: 'hello vue',
    },
    mutations: {
        INCREMENT(state, value) {
            state.count += value;
        }
    },
    actions: {
        increment(context, value) {
            context.commit('INCREMENT', value);
        }
    },
    getters: {
        bigCount(state) {
            return state.count * 10
        }
    }
}

const test2 = {
    namespaced: true, //开启命名空间
    state: {},
    mutations: {},
    actions: {},
    getters: {}
}


export default new Vuex.Store({
    modules: { test1, test2 } // 导入模块
});
```



**组件内:**

```vue
<template>
  <div class="count">
    <h2>计数:</h2>
    <div>
      {{ count }}
    </div>
    <div>放大10倍后: {{ bigCount }}</div>
    <div>你好:{{ hello }}</div>
    <input type="text" v-model.number="num" />
    <button @click="increment(num)">增加</button>
  </div>
</template>

<script>
// 导入 vuex 提供的 map 方法
import { mapState, mapGetters, mapActions, mapMutations } from "vuex";

export default {
  name: "TestVue",
  data() {
    return {
      num: 1,
    };
  },
  methods: {
    // 简写 dispatch
    //
    // 对象简写
    // ...mapActions("test1", { increment: "increment" }),
    //
    // 数组简写
    ...mapActions("test1", ["increment"]),
    //
    // 原始vue写法
    // increment() {
    //   // 如果vuex采用模块化, 那么原始vue将使用 / 作为命名空间和触发指定状态的分割符
    //   // 斜杠 / 前为模块名, 斜杠 / 后为需要触发的状态名
    //   return this.$store.dispatch("test1/increment", this.num);
    // },
  },
  computed: {
    // 使用vuex提供的map简化计算属性
    ...mapState("test1", ["count", "hello"]),
    ...mapGetters("test1", ["bigCount"]),
  },
};
</script>

<style lang="sass" scoped>
.count
  margin-top: 30px
  margin-left: 30px

  div
    padding: 5px 0
</style>
```
