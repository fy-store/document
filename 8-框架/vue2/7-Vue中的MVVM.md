## Vue中的MVVM

**MVVM模型:**

1.M：模型(Model) ：data中的数据

2.V：视图(View) ：模板代码

3.VM：视图模型(ViewModel)：Vue实例



**观察发现：**

1.data中所有的属性，最后都出现在了vm身上。

2.vm身上所有的属性 及 Vue原型上所有属性，在Vue模板中都可以直接使用。