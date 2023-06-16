## 3.Vue中的数据代理

**1.Vue中的数据代理：**

通过vm对象来代理data对象中属性的操作（读/写）



**2.Vue中数据代理的好处：**

更加方便的操作data中的数据



**3.基本原理：**

vue2 是通过 `Object.defineProperty()` 实现数据代理 , 把 data 对象中所有属性添加到 vm 上。

为每一个添加到 vm 上的属性，都指定一个 getter/setter。

在 getter/setter 内部去操作（读/写）data 中对应的属性。