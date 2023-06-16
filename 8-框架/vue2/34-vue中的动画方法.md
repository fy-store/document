## Vue封装的过度与动画

**作用：**

在插入、更新或移除 DOM 元素时，在合适的时候给元素添加样式类名。



**写法：**

此处 `v` 可通过自己指定的 `name` 来变更前缀

事先准备好样式：

- 元素进入的样式类名：

  - v-enter：进入的起点

  - v-enter-active：进入过程中(通常用这个)

  - v-enter-to：进入的终点

- 元素离开的样式类名：

  - v-leave：离开的起点

  - v-leave-active：离开过程中(通常用这个)

  - v-leave-to：离开的终点



**单个元素:**

单个元素使用动画使用 `<transition>` 元素包裹要过度的元素，并配置 `name` 属性 , 若不配做 `name` 则默认使用 `v` 前缀开头的类名

`appear` 初始渲染时带有过渡模式 + 动画出现

```vue
<template>
  <div>
    <transition name="move" appear>
      <div v-show="isShow" class="move-to"></div>
    </transition>
    <button @click="isShow = !isShow">显示隐藏</button>
  </div>
</template>

<script>
export default {
  name: "TestVue",
  data() {
    return {
      isShow: true,
    };
  },
};
</script>

<style scoped>
.move-to {
  position: absolute;
  top: 80px;
  left: 0;
  width: 200px;
  height: 200px;
  background-color: #f40;
  transition: 0.3s linear;
  opacity: 1;
}

.move-enter-active,
.move-leave-active {
  transform: translateX(600px);
  opacity: 0;
}
</style>
```



**多个元素:**

若有多个元素需要动画过度，则需要使用：`<transition-group>` 元素，且每个元素都要指定 `key` 值。

```vue
<template>
  <div>
    <transition-group name="move" appear>
      <div v-show="isShow" class="move-to" key="001"></div>
      <div v-show="isShow" class="move-to" key="002"></div>
    </transition-group>
    <button @click="isShow = !isShow">显示隐藏</button>
  </div>
</template>

<script>
export default {
  name: "TestVue",
  data() {
    return {
      isShow: true,
    };
  },
};
</script>

<style scoped>
.move-to {
  position: absolute;
  top: 80px;
  left: 0;
  width: 200px;
  height: 200px;
  background-color: #f40;
  transition: 0.3s linear;
  opacity: 1;
}



.move-enter-active,
.move-leave-active {
  transform: translateX(600px);
  opacity: 0;
}
</style>
```

