## flex 弹性盒（css3）`*`

> display: flex;

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/CSS_Flexible_Box_Layout/Basic_Concepts_of_Flexbox" target="_blank">MDN文档</a> 

flex 是一种一维布局，一次只能处理一个维度上的元素布局，一行或者一列 。

当使用 flex 布局时，它有两个轴，分为 主轴 和 侧轴 。

默认情况下 主轴对应X轴，侧轴对应Y轴；当然这是可以更改的。

使用 flex 后会产生以下默认情况：

- 元素排列为一行 `flex-direction` 属性的初始值是 `row` 。
- 元素从主轴的起始线开始 。
- 元素不会在主维度（主轴）方向拉伸，但是可以缩小（默认父容器主轴方向空间不够子容器被压缩）。
- 元素被拉伸来填充交叉轴（侧轴默认撑满）大小 。
- `flex-basis` 属性为 `auto`。
- `flex-wrap` 属性为 `nowrap`（默认容器超出不换行）。
- 它的直系子元素的 `displaay` 将会被改变为 `block` 。

 



### flex-direction 设置主轴

> flex-direction

使用该属性定义主轴方向，另一侧轴则垂直于主轴。

该属性定义了主轴上容器的排列方式。

主轴由 `flex-direction` 定义，可以取 4 个值：

- `row` 自左向右（默认）
- `row-reverse` 自右向左
- `column` 自上到下
- `column-reverse` 自下向上

 



### flex-wrap 子容器是否允许换行

> flex-wrap

可以取 3 个值：

- `nowrap` 不允许换行（默认）
- `wrap` 允许换行
- `wrap-reverse`  类似主轴被设置了自下向上后的 wrap

 



### flex-flow 简写属性

> *flex-flow* 属性是 flex-direction 和 flex-wrap 的简写

语法：`flex-flow: flex-direction flex-wrap;`

填写两个参数：

- 第一个设置 flex-direction
- 第二个设置 flex-wrap

 



### flex-grow 子容器分配剩余空间

> flex-grow

设置子容器对剩余空间应分配比例，是宽是高取决于主轴的方向。

该属性给需要的子容器设置，若其他子容器也设置则按设置的比例进行分配。

语法：`flex-grow: number;`   0 - 正无穷，默认为 0

 



### flex-shrink 子容器超出父容器时的收缩规则

> flex-shrink

语法：`flex-shrink: number;`  0 - 正无穷，默认值为 1

设置  flex-shrink: 0; 则超出时不进行收缩

 



### flex-basis 设置主轴容器初始大小

> flex-basis

语法：`flex-basis: auto/像素大小;` 默认值 auto

将容器初始设置为 0 , 而后使用 flex-grow 平分容器, 可以实现等分布局

 



### flex 简写属性

> flex

语法：`flex: flex-grow [flex-shrink] [flex-basis];`

依次顺序对应。

flex: none;  ===  flex: 0 0 auto; 子容器超出父容器时不收缩。

 



### align-items 侧轴排列方式（单行）

> align-items

常用取值：

- normal 默认值 弹性盒中等同 align-items: stretch;
- stretch 子容器在侧轴没有大小则被拉伸至行高
- flex-start 子容器在侧轴的起点排列
- flex-end 子容器在侧轴的终点排列
- center 子容器在侧轴居中排列
- 等等

 



### align-content 侧轴排列方式（多行）

> align-content

设置侧轴线间内容的排列方式，即多行容器的排列方式，仅对多行有效，单行无效。

常用取值：

- normal 默认值 弹性盒中等同 flex-start

- flex-start 子容器在侧轴起点排列

- flex-end 子容器在侧轴终点排列

- center 子容器在侧轴居中排列

- space-around 子容器在侧轴平分剩余空间（等分排列）

- space-between 子容器在侧轴先两边贴边，再平分剩余空间

- stretch 在侧轴子容器平分侧轴父容器大小（宽/高）
- 等等

 



### justify-content 主轴排列方式

> justify-content

取值：

- normal 默认值
- flex-start 子容器在主轴起点排列

- flex-end 子容器在主轴终点排列

- center 子容器在主轴居中排列

- space-around 子容器平分剩余空间（等分排列）

- space-between 子容器先两边贴边 再平分剩余空间

 



### align-self 设置单个容器侧轴排列方式

> align-self

align-self 控制子容器在侧轴的排列方式

 align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖 align-items 属性

常用取值：

- normal 默认值 弹性盒中等同 align-items: stretch;
- auto 继承父容器的 align-items

- stretch 子容器在侧轴没有大小则被拉伸至行高
- flex-start 子容器在侧轴的起点排列
- flex-end 子容器在侧轴的终点排列
- center 子容器在侧轴居中排列
- 等等

 



### order 设置子容器排列次序

> order

只是视觉上的变更，不会改变逻辑上和结构上次序。

语法：`order: number;` 需为整形数字，正负皆可，默认值 0

数组越小，排列越靠前，示例：order：-1;