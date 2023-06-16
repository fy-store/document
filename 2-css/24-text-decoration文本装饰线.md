## text-decoration 文本装饰线

> 设置文本装饰线

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration" target="_blank">MDN文档</a> 

**简写：**text-decoration: underline green solid;

当然默认就是 solid，所以可以省略；颜色默认跟随字体，也可以省略；

text-decoration 简写的具体属性为：

`text-decoration-line`  装饰线类型

 `text-decoration-color`  装饰线颜色

`text-decoration-style`  装饰线的样式

- 装饰线类型：
  - none 没有装饰线
  - underline 下划线
  - overlien 上划线
  - line-through 删除线
- 装饰线样式：
  - solid 实线
  - double 双实线
  - 其余同 border 类似
  - <a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/text-decoration-style" target="_blank">MDN文档</a> 

另外一个属性：`text-decoration-thickness` 设置装饰线的粗细程度

- 取值：
  - auto 自动
  - from-font 跟随字体文件首选厚度
  - 具体像素值