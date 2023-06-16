## 路由

**理解：** 

一个路由（route）就是一组映射关系（key - value），多个路由需要路由器（router）进行管理。



**前端路由：**

key是路径，value是组件。



**注意点:**

1. 路由组件通常存放在 `pages` 文件夹，一般组件通常存放在 `components` 文件夹。
2. 通过切换，“隐藏”了的路由组件，默认是被销毁掉的，需要的时候再去挂载。
3. 每个组件都有自己的 `$route` 属性，里面存储着自己的路由信息。
4. 整个应用只有一个 router，可以通过组件的 `$router` 属性获取到。





## 使用准备

**安装vue-router，命令：**

```npm
npm i vue-router@3
or
yarn add vue-router@3
```



**应用插件：**

`main.js`

```js
import Vue from 'vue'
import App from './App.vue'
// 引入 vue路由
import VueRouter from 'vue-router'
// 引入配置的路由规则
import router from './router'

// 应用插件
Vue.use(VueRouter) 

Vue.config.productionTip = false

new Vue({
  el: '#app',
  render: h => h(App),
  router // 挂载路由
})
```



配置路由规则:

在 src 下创建 `router/index.js`

```js
// 引入路由器, 用于管理路由
import VueRouter from "vue-router";

// 引入组件
import Home from "../components/Home";
import About from "../components/About";

// 创建一个路由器
const router = new VueRouter({
    routes: [
        // 放置一组一组路由规则
        {
            path: '/home',
            component: Home
        },
        {
            path: '/about',
            component: About
        },
    ],
})

export default router;
```





## 基础使用

**编写router配置项:**

```js
//引入VueRouter
import VueRouter from 'vue-router'
//引入Luyou 组件
import About from '../pages/About'
import Home from '../pages/Home'

//创建router实例对象，去管理一组一组的路由规则
const router = new VueRouter({
	routes:[
		{
			path:'/about',
			component:About
		},
		{
			path:'/home',
			component:Home
		}
	]
})

//暴露router
export default router
```





**使用 router-link 配置路由跳转:**

使用属性 `to` 指定跳转的组件

router-link 最终会转为 `a` 元素

使用特殊属性 `active-class` 即元素激活时的样式

```vue
<router-link active-class="active" to="/about">About</router-link>
```





**指定展示位置:**

```vue
<router-view></router-view>
```





**组件中:**

LinkNav 组件

```vue
<template>
  <div>
    <ul class="list">
      <!-- <li><a href="#">home</a></li>
      <li><a href="#">about</a></li> -->
      <li>
        <router-link active-class="active" to="/home">home</router-link>
      </li>
      <li>
        <router-link active-class="active" to="/about">about</router-link>
      </li>
    </ul>
    <!-- 路由展示的位置 -->
    <div class="show">
        <h2>展示内容</h2>
        <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style lang="sass" scoped>
.list
    width: 400px
    li
        margin-bottom: 5px
        cursor: pointer

        a
            display: block
            width: 100%
            height: 100%
            padding: 5px 10px
            background-color: #ccc

        a.active
            background-color: #f40
            color: #fff
</style>
```



**pages目录下:**

路由组件存放的目录



Home 组件

```vue
<template>
  <div>home</div>
</template>

<script>
export default {

}
</script>

<style>

</style>
```



About 组件

```vue
<template>
  <div>about</div>
</template>

<script>
export default {

}
</script>

<style>

</style>
```





## 多级路由(嵌套路由)

配置路由规则，使用children配置项



**路由配置:**

```js
// 引入路由器, 用于管理路由
import VueRouter from "vue-router";

// 引入组件
import Home from "../pages/Home";
import About from "../pages/About";
import Person from "../pages/Person";
import Region from "../pages/Region";


// 创建一个路由器
const router = new VueRouter({
    routes: [
        // 放置一组一组路由规则
        {
            path: '/home',
            component: Home
        },
        {
            path: '/about',
            component: About,
            children: [
                {
                    path: 'person', // 多级路由下不再需要 / 开头
                    component: Person
                },
                {
                    path: 'region',
                    component: Region
                }
            ]
        },
    ],
})

export default router;
```

**组件中使用:**

```vue
<template>
  <div>
    <h2>about</h2>
    <ul>
        <!-- 多级路由使用 -->
      <li><router-link to="/about/person">展示人员</router-link></li>
      <li><router-link to="/about/region">展示地区</router-link></li>
    </ul>
    <router-view></router-view>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>
```





## 路由的query参数

**组件使用传参:**

```vue
<template>
  <div>
    <ul>
      <li>
        <!-- 查询字符串形式传参 query -->
        <router-link
          to="/about/person/personInfo?name=小明&age=18&address=广东"
        >
          小明
        </router-link>
      </li>
      <li>
        <!-- 对象形式传参 query -->
        <router-link
          :to="{
            path: '/about/person/personInfo',
            query: {
              name: '小李',
              age: 19,
              address: '广东',
            },
          }"
        >
          小李
        </router-link>
      </li>
      <li>
        <router-link
          to="/about/person/personInfo?name=小张&age=20&address=广东"
        >
          小张
        </router-link>
      </li>
    </ul>
    <router-view></router-view>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>
```



**接受参数:**

```vue
<template>
  <div>
    <div>姓名: {{ $route.query.name }}</div>
    <div>年龄: {{ $route.query.age }}</div>
    <div>住址: {{ $route.query.address }}</div>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>
```





## 命名路由

用于简化路径书写



**命名:**

```js
{
    path: 'person',
    component: Person,
    children: [
        {
            name: 'personInfo', // 命名路由
            path: 'personInfo',
            component: PersonInfo
        }
    ]
},
```



**组件使用命名路由:**

```vue
<li>
    <router-link
      :to="{
        name: 'personInfo', // 使用命名路由
        query: {
          name: '小张',
          age: 20,
          address: '广东',
        },
      }"
    >
  		小张
	</router-link>
</li>
```





## 路由的params参数

**路由规则:**

```js
{
    name: 'personInfo', // 命名路由
    // 当使用 params 路由传参时需告知路由器
    // 使用占位符声明接收params参数
    path: 'personInfo/:name/:age/:address', 
    component: PersonInfo
}
```



**组件传递params参数:**

```vue
<ul>
  <li>
    <!-- 对象形式传参 params -->
    <router-link
      :to="{
        name: 'personInfo',
        params: {
          name: '小李',
          age: 19,
          address: '广东',
        },
      }"
    >
      小李
    </router-link>
  </li>
  <li>
      <!-- 地址栏手动拼接形式传参 params -->
    <router-link
      :to="{
        path: '/about/person/personInfo/小张/20/广东',
      }"
    >
      小张
    </router-link>
  </li>
</ul>
```



**使用params参数:**

组件中

```vue
<template>
  <div>
    <div>姓名: {{ $route.params.name }}</div>
    <div>年龄: {{ $route.params.age }}</div>
    <div>住址: {{ $route.params.address }}</div>
  </div>
</template>

<script>
export default {};
</script>

<style>
</style>
```





## 路由的props配置

用于路由传参



**第一种 props 传参:**

对象形式, 用的少, 因为是死数据

当 `props` 是一个对象时，它将原样设置为组件 props。当 props 是静态的时候很有用。



*路由中:*

```js
{
    name: 'personInfo',
    path: 'personInfo',
    component: PersonInfo,
    // props 传参
    props: {
        from: 'china'
    }
}
```



*组件中接收使用:*

```vue
<template>
  <div>
    <div>来自: {{ from }}</div>
  </div>
</template>

<script>
export default {
  props: ["from"],
};
</script>
```



**第二种 props 传参:**

布尔值形式, 若为 true , 则会将路由组件接受到的所有 params 参数, 以 props 形式传递给组件

当 `props` 设置为 `true` 时，`route.params` 将被设置为组件的 props。



*路由中:*

```js
{
    name: 'personInfo',
    path: 'personInfo',
    component: PersonInfo,
    props: true
}
```



*组件传参:*

组件中传递 params 参数 , 或者路由规则中传递 params 参数

```vue
<li>
    <router-link
      :to="{
        name: 'personInfo',
        params: {
          name: '小张',
          age: 20,
          address: '广东',
        },
      }"
    >
      小张
    </router-link>
</li>
```



*组件中接收使用:*

```vue
<template>
  <div>
    <div>姓名: {{ name }}</div>
    <div>年龄: {{ age }}</div>
    <div>住址: {{ address }}</div>
  </div>
</template>

<script>
export default {
  props: ["name", "age", "address"],
};
</script>
```





**第三种 props 传参:**

使用函数形式 , 支持 query , params 传参 , 最强大的写法

你可以创建一个返回 props 的函数。这允许你将参数转换为其他类型，将静态值与基于路由的值相结合等等。



*路由中:*

```js
{
    name: 'personInfo',
    path: 'personInfo',
    component: PersonInfo,
    props($route) {
        return {
            from: 'china',
            ...$route.query
        }
    }
}
```



*传参:*

```vue
<li>
    <router-link
      :to="{
        name: 'personInfo',
        query: {
          name: '小李',
          age: 19,
          address: '广东',
        },
      }"
    >
      小李
    </router-link>
</li>
```



*组件中接收使用:*

```vue
<template>
  <div>
    <div>姓名: {{ name }}</div>
    <div>年龄: {{ age }}</div>
    <div>住址: {{ address }}</div>
    <div>来自: {{ from }}</div>
  </div>
</template>

<script>
export default {
  props: ["name", "age", "address", "from"],
};
</script>
```





##  router-link 的replace属性

**作用：**

控制路由跳转时操作浏览器历史记录的模式



**浏览器的历史记录有两种写入方式：**

分别为 ```push``` 和 ```replace``` ，```push``` 是追加历史记录，```replace``` 是替换当前记录。路由跳转时候默认为 ```push```



**如何开启 ```replace``` 模式：**

```<router-link replace>首页</router-link>```





## 编程式路由导航

即不借助 `<router-link></router-link>` 来进行路由跳转

使用 `$router` 原型上的方法 `push` 和 `replace`

*其他方法:*

```js
// 向前移动一条记录，与 router.forward() 相同
router.go(1)

// 返回一条记录，与 router.back() 相同
router.go(-1)

// 前进 3 条记录
router.go(3)

// 如果没有那么多记录，静默失败
router.go(-100)
router.go(100)
```



**组件中:**

```vue
<template>
  <div>
    <ul class="list">
      <li>
        <button @click="home">home</button>
      </li>
      <li>
        <button @click="about">about</button>
      </li>
    </ul>
    <!-- 路由展示的位置 -->
    <div class="show">
      <h2>展示内容</h2>
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  methods: {
    home() {
      this.$router.push({
        name: "home",
        query:{}
      });
    },
    about() {
      this.$router.push({
        name: "about",
        params:{}
      });
    },
  },
};
</script>
```



**注意点:**

在跳转路由按钮中点击多次会产生报错 , 是因为我们没有对跳转做而外处理

vue-router@3.0版本及以上回调形式已经改成promise api的形式了，返回的是一个promise，如果路由地址跳转相同, 且没有捕获到错误，那么报错 .



**解决方法1:**

让其捕获错误

```js
 methods: {
    goSearch() {
      this.$router.push("/search").catch(() => {});
    },
  },
```



**解决方法2:**

在 main.js 下注册一个全局函数即可 （注：此处理方案只针对于vue-router 3.0以上版本！！！）

```js
import Router from 'vue-router'

const originalPush = Router.prototype.push
Router.prototype.push = function push(location) { 
   
  return originalPush.call(this, location).catch(err => err)
}

// 注：官方vue-router@3.0及以上新版本路由默认回调返回的都是promise，原先就版本的路由回调将废弃！！！！
```





## 缓存路由组件

**作用:**

让不展示的路由组件保持挂载，不被销毁。

`include="Home"` 指定需要缓存的组件, 此处的 `home` 是 **`组件名`** , 若不书写将会把所有在此处显示的组件都缓存

缓存多个 , 写出数组形式 `include="[Home, About]"` 或 `include="Home, About"`

注意是组件名

它会根据组件的 [`name`](https://cn.vuejs.org/api/options-misc.html#name) 选项进行匹配，所以组件如果想要条件性地被 `KeepAlive` 缓存，就必须显式声明一个 `name` 选项。

官方文档: https://cn.vuejs.org/guide/built-ins/keep-alive.html#include-exclude



**示例:**

```vue
<keep-alive include="Home"> 
    <router-view></router-view>
</keep-alive>
// or
<KeepAlive include="Home"> 
    <router-view></router-view>
</KeepAlive>
```





## 两个新的生命周期钩子

路由组件独有的生命周期钩子 , 在路由组件中配置

两个钩子只有路由组件使用了 `KeepAlive` 进行缓存时才会触发



**作用：**

路由组件所独有的两个钩子，用于捕获路由组件的激活状态。



**具体：**

- ```activated``` 路由组件被激活时触发。

- ```deactivated``` 路由组件失活时触发。





## 路由守卫

**作用：**

对路由进行权限控制



**分类：**

全局守卫、独享守卫、组件内守卫



**路由守卫接收到的三个参数:**

- `to` 何处来
- `from` 去往何处
- `next` 调用则放行(后置路由守卫没有 next 函数)



### 全局路由守卫

**路由中:**

```js
// 引入路由器, 用于管理路由
import VueRouter from "vue-router";

// 引入组件
import Home from '../pages/Home'
import About from '../pages/About'



// 创建一个路由器
const router = new VueRouter({
    routes: [
        // 放置一组一组路由规则
        {
            name: 'home',
            path: '/home',
            component: Home,
            // meta 路由元信息
            meta: {
                // 自己写一些字段, 用于给该路由进行一些数据标识
                isAuth: true
            }
        },
        {
            name: 'about',
            path: '/about',
            component: About
        }
    ],
})

// 全局前置路由守卫
// 每一次切换路由前一刻调用 和 初始化时调用一次
router.beforeEach((to, from, next) => {
    // to 何处来
    // from 去往何处
    console.log('全局前置路由守卫: ', '路由切换了');
    if (to.meta.isAuth) {
        // 此处进行权限校验
    }
    next(); // 需进行放行
})

// 全局后置路由守卫
// 每一次切换路由后调用 和 初始化时调用一次
router.afterEach((to, from) => {
    // 后置路由守卫没有 next 函数
    console.log('全局后置路由守卫: ', '路由切换了');
})

export default router;
```





### 独享路由守卫

某一个路由所单独享用的路由守卫

独享路由守卫只有前置没有后置



**路由中:**

```js
{
    name: 'about',
    path: '/about',
    component: About,
    // 进入该路由前一刻
    beforeEnter(to, from, next) {
        console.log('独享路由守卫: ', '路由切换了');
        next()
    }
}
```





### 组件内路由守卫

在组件内写路由守卫, 而不是在路由配置文件中书写



**组件中:**

```vue
<template>
  <div>
    <h2>这是home</h2>
    <div>
      <input type="text" /><br />
      <input type="text" /><br />
      <input type="text" /><br />
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  //通过路由规则，进入该组件前一刻被调用
  beforeRouteEnter(to, from, next) {
    console.log("组件路由守卫: ", "想要进入该组件");
    // 不放行进入不了组件
    next();
  },
  //通过路由规则，离开该组件前一刻被调用
  beforeRouteLeave(to, from, next) {
    // 不放行离开不了组件
    console.log("组件路由守卫: ", "想要离开该组件");
    next();
  },
};
</script>
```





## 路由器的两种工作模式

**简介:**

- 对于一个url来说，什么是hash值？—— #及其后面的内容就是hash值。

- hash值不会包含在 HTTP 请求中，即：hash值不会带给服务器。

- hash模式：

  - 地址中永远带着#号，不美观 。

  - 若以后将地址通过第三方手机app分享，若app校验严格，则地址会被标记为不合法。

  - 兼容性较好。

- history模式：

  - 地址干净，美观 。

  - 兼容性和hash模式相比略差。

  - 应用部署上线时需要后端人员支持，解决刷新页面服务端404的问题。



**更改模式:**

路由中

```js
// 引入路由器, 用于管理路由
import VueRouter from "vue-router";

// 引入组件
import Home from '../pages/Home'
import About from '../pages/About'



// 创建一个路由器
const router = new VueRouter({
    mode: 'history', // 更改路由器工作模式, 默认为 hash 模式
    routes: [
        {
            name: 'home',
            path: '/home',
            component: Home,
        },
        {
            name: 'about',
            path: '/about',
            component: About,
        }
    ],
})
export default router;
```



**node中解决history报错问题的包:**

包名: *connect-history-api-fallback*





## 路由重定向

**路由中:**

```js
const router = new VueRouter({
    routes: [
        {
            // 路由重定向
            path: '/', // / 或者 *
            redirect: '/home' // 当访问 / 时, 重定向至 /home
        },
        {
            path: '/home',
            component: Home
        },
        {
            path: '/login',
            component: Login
        },
        {
            path: '/register',
            component: Register
        },
        {
            path: '/search',
            component: Search
        }
    ]
})
```

