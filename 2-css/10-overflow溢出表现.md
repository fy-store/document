## overflow 溢出表现形式

> 设置内容溢出容器时的表现形式

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/overflow" target="_blank">MDN文档</a> 

简写：`overflow`

具体属性：`overflow-x` 和 `overflow-y`

- visible 默认值
- hidden 溢出隐藏
- scroll 显示滚动条，无论内容是否溢出
- auto 自动 内容溢出时显示滚动条，不溢出不显示

**注意：**

设置一个轴为`visible`（默认值），同时设置另一个轴为不同的值，会导致设置`visible` 的轴的行为会变成 `auto`。

即使将 overflow 设置为 hidden，也可以使用 JavaScript `Element.scrollTop` 属性来滚动 HTML 元素。