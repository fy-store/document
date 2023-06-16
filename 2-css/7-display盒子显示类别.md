## 盒子显示类别 

 <a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/display" target="_blank">MDN文档</a> 

display 属性的值不止 `block` `inline` `inline-block` `none`

但是这几个是非常具有代表性的 , 后面还会有用于布局的 `flex` `grid` 和其他一些属性值



### block

> 块盒

块盒：`display:block;`

**特点：**

- 可以设置宽高
- 可以设置内外边距
- 可以设置边框
- 默认情况下独占一行
- 默认情况下宽度撑满整个父盒子



### inline

> 行盒

行盒：`display:inline;`

**特点：**

- 不独占一行
- 内容决定大小
- 内边距：水平方向有效，垂直方向仅会影响背景，不会实际占据空间
- 边框：水平方向有效，垂直方向不会占据实际空间
- 外边距：水平方向有效，垂直方向不会实际占据空间

注意点：

调整行盒的宽高，应该使用字体大小 行高 字体类型 间接调整。

给父盒子设置 `text-align:center;` 可以实现内部行盒水平居中



### inline-block

>行块盒

行块盒：`display:inline-block;`

**特点：**

- 不独占一行
- 盒模型中所有尺寸都有效
- `margin:auto;` 无效，`text-align:center;` 有效

**注意点：**

如果使用<u>行块盒</u>进行布局需注意多个盒子间的空格，可以采用删除换行或者`font-size:0;` 解决



### none

> 隐藏盒子

隐藏盒子：`display:none;`

设置为 none 后，盒子将从页面消失，位置也不在占有

对于 `display:none;` 的元素，浏览器渲染引擎不会将其解析到布局树上