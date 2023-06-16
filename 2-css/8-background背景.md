## background 背景

> background 背景

关于何时使用背景：

当图片属于网页内容时，使用img图片

当图片仅用于美化页面时，使用背景图

简写：`background: url(...) no-repeat 0 0/100% #000 ...;`

简写属性位置和大小同时出现时需要以 `/` 进行分割，前面为位置，后面为大小，以便浏览器辨识

背景和颜色可以同时设置，颜色将会在图层最底，图片透明或失效时将显示颜色。

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/background" target="_blank">MDN文档</a>

具体属性如下：



### background-color

> 设置背景颜色

背景颜色和背景图片可以一起设置，当图片失效或者透明时会显示背景颜色

按层次来看，背景颜色在背景图片之下

```css
background-color: #000;
```



### background-image

> 设置一个或多个背景图片
>
> 属性：

- none 默认值
- url(...) 背景图，设置一个或多个，以逗号分割

```css
background-image: url(...),url(...);
```



### background-repeat

> 设置背景的重复方式

- repeat 两个轴重复
  - repeat-x 单独重复x轴
  - repeat-y 单独重复y轴
- no-repeat 不重复
- 其他属性查阅文档

一个值：设置两个轴

两个值：设置分别的轴

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-repeat" target="_blank">MDN文档</a>



### background-size

> 设置背景的大小

关键字：

auto 等比例缩放 默认值

contain 等比例缩放，尽可能铺满盒子，碰到一个边即停止，有可能会留白

cover 等比例缩放，铺满整个盒子，有可能会溢出

也可以具体数值

一个值：设置宽，高则为 auto

两个值：设置宽 高



### background-clip

> 设置元素的背景（背景图片或颜色）是否延伸到边框、内边距盒子、内容盒子下面

- border-box 背景延伸至边框外沿（但是层次在边框下）

- padding-box 背景延伸至内边距外沿，不会绘制到边框处

- content-box 背景被裁剪至内容区内（content box）

- text 背景被裁剪成文字的前景色（css3新增属性）

  - 实际就是图片只会在文字内显示，超出文字的会被隐藏
  - 可以实现渐变文字等

  ```css
  background-clip: text;
  -webkit-background-clip: text;
  color: transparent;
  ```



### background-position

> 设置背景图片的位置，相对于原点，默认原点左上角

可以使用方位关键字：top 、right 、bottom 、left

也可以使用具体的像素位置 px % 等

一个值：设置到某个位置，另一个轴居中

两个值：x轴 和 y轴

更多用法：

距离下边 50px 距离右边 100px

```css
background-position: bottom 50px right 100px;
```

可用于精灵图（雪碧图）



### background-origin `-`

> 设置背景图片相对的原点位置

- border-box
- padding-box 默认值
- content-box



### background-attachment `-`

> 设置当容器内滚动时，背景图的表现形式

用于制作滚动视差

- fixed 相对视口固定
- local 相对内容固定
- scroll 相对元素本身固定 默认值

支持设置多背景，使用 , 逗号分割，与每个背景一一对应

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-origin" target="_blank">MDN文档</a> 