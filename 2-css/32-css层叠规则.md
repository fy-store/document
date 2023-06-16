## css 层叠规则 `*`

> 层叠规则

<a href="https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Cascade_and_inheritance" target="_blank">MDN文档</a> 

**声明冲突：** 同一个样式，多次应用到同一元素

**层叠：** 解决声明冲突的过程，浏览器自动处理（权重计算）

**层叠规则：**

- *比较重要性*

  - 重要性从高到低
  - 作者样式表：开发者书写的样式
  - 作者样式表中的 !important
  - 作者样式表中的普通样式
  - 浏览器默认样式表中的样式

- *比较特殊性*

  - 权重：
  - !impotant             infinity 正无穷大
  - 行间样式                1000
  - id                             100
  - class, 属性, 伪类    10
  - 标签 伪元素           1
  - 通配符                    0

  之间的进制为256 ，比较方法（千, 百, 十, 个）从千位开始比较 或 直接数值相加

- *比较源次序*

  - 代码书写靠后的胜出
  - 后面覆盖前面