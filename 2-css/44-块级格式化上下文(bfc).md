## 块级格式化上下文(bfc)

> 全称 Block Formatting Context 简称 bfc

<a href="https://developer.mozilla.org/zh-CN/docs/orphaned/Web/Guide/CSS/Block_formatting_context" target="_blank">MDN文档</a> 

*它是一块独立的渲染区域，它规定了该区域中，常规流块盒的布局*

- 常规流块盒在水平方向上，必须撑满包含块
- 常规流块盒在包含块的垂直方向上依次摆放
- 常规流块盒若外边距无缝相邻，则进行外边距合并
- 常规流盒子的自动高度和摆放位置，无视浮动元素

*bfc渲染区域：*

这个区域由某个html元素创建，以下元素会在其内部创建bfc区域：

- 根元素 意味着， 元素创建的bfc区域，覆盖了网页中所有的元素
- 浮动元素
- 绝对定位元素  
- overflow不等于visible的块盒

不同的bfc区域，它们进行渲染时互不干扰

创建bfc的元素，隔绝了它内部和外部的联系，内部的渲染不会影响到外部

创建bfc的元素，不会和它的子元素进行外边距合并(margin 塌陷)

 bfc可以去掉浮动副作用，但会带来一系列其他效果；清除浮动的方式的副作用最小（推荐）