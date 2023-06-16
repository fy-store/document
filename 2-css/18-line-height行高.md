### line-height

> 设置行高

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height" target="_blank">MDN文档</a> 

每行文本的高度，该值越大，每行文本的距离越大。

设置行高为容器的高度，可以让单行文本垂直居中。

行高可以设置为纯数字，表示相对于当前元素的字体大小。



**行高可以继承：**

- 带单位：
  - 可以px em 百分比 等 （取值为字体的多少）
  - 以上先计算后得出具体px数值再继承
- 不带单位：
  - 行高可以不带单位
  - line-height: 1.5; 行高是字体的1.5倍
  - 继承方式为直接继承再进行计算具体数值