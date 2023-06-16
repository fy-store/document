## transform 2D和3D变换

> transform: \<transform-function>

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform" target="_blank">MDN文档</a> 

通过 `transform` 可以实现很多视觉盛宴

`transform` 只作用在块盒和行块盒上, 行盒不生效

`transform` 通常会结合 过渡 `transition` 或者 动画 `animation` 一同使用





## 位移 translate

>  translate

 <a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/translate" target="_blank">MDN文档</a> 

translate 允许单独声明平移变换，并独立于 transform 属性。这样就无需在 transform 中声明该函数并记住转换函数的确切顺序了 .



**语法:**

```css
/* 不平移 */
translate: none;

/* 一个值 */
translate: 100px;

/* 两个值 */
translate: 100px 200px;

/* 三个值 */
translate: 100px 100px -100px;
```



- 一个值为简写 `x` 和 `y` 轴
- 两个值分别设置 `x` 和 `y`
- 三个值分别设置 `x` 和 `y` 和 `z` 轴

*注意:*

当设置了 `z` 轴后, 需要在该元素或其祖先元素上设置景深属性 `perspective` , 否则 `z` 轴将不产生效果

一般的, 如果设置了 `z` 轴, 通常会将元素设置在3D空间中 , 可以通过在该元素或其祖先元素上设置 `transform-style: preserve-3d` 



**示例:**

```css
.box {
    perspective: 1000px;
    transform-style: preserve-3d;
	translate: 50px 100px -100px;
}
```





## 位移 translate()

> transform: translate()

该位移方法设置在 `transform` 上

在 transform 中设置位移时应始终将 translate() 放置在第一个, 否则将发送错乱 .



**语法:**

```css
/* 设置 x 轴*/
transform: translateX(100px);

/* 设置 y 轴*/
transform: translateY(100px);

/* 设置 z 轴*/
transform: translateZ(100px);

/* 同时设置 x 和 y 轴 */
transform: translate(100px, 100px);

/* 同时设置 x 和 y 和 z 轴 */
transform: translate3d(100px, 100px, -100px);
```



*注意:*

当设置了 `z` 轴后, 需要在该元素或其祖先元素上设置景深属性 `perspective` , 否则 `z` 轴将不产生效果

一般的, 如果设置了 `z` 轴, 通常会将元素设置在3D空间中 , 可以通过在该元素或其祖先元素上设置 `transform-style: preserve-3d` 





**示例:**

```css
.box {
    perspective: 1000px;
    transform-style: preserve-3d;
}

.child {
    transform: translate3d(100px, 100px, -100px);
}
```





##  旋转 rotate()

> transform: rotate()

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-function/rotate" target="_blank">MDN文档</a> 

将元素围绕一个定点进行旋转, 这个定点可以通过 `transform-origin` 指定, 默认为元素正中心

旋转中设置的值采用角度来进行设置, 单位为 `deg` 或 `turn`



**语法:**

```css
/* 围绕 x 轴进行旋转 */
transform: rotateX(35deg);

/* 围绕 y 轴进行旋转 */
transform: rotateY(35deg);

/* 围绕 z 轴进行旋转 */
transform: rotateZ(35deg);

/* 设置 x y z 轴旋转 */
transform: rotate3d(1, 2.0, 3.0, 10deg);
```



*注意:*

旋转我们通常会结合 设置转换中心 `transform-origin` 和 设置景深 `perspective` 和 设置 3d空间 `transform-style: preserve-3d` 一起配合使用





## 缩放 scale

> scale

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/scale" target="_blank">MDN文档</a> 

scale 允许单独声明缩放变换，并独立于 transform 属性。这样就无需在 transform 中声明该函数并记住转换函数的确切顺序了 .



**语法:**

```css
/* 不缩放 */
scale: none;

/* 一个值 */
scale: 0.5;

/* 两个值 */
scale: 2 0.5;

/* 三个值 */
scale: 2 0.5 2;
```



- 一个值为简写 `x` 和 `y` 轴的缩放
- 两个值为分别设置 `x` 和 `y` 轴的缩放
- 三个个值为分别设置 `x` 和 `y` 和 `z` 轴的缩放



*注意:*

缩放设置直接填写缩放的比例 

正常大小为 `1` 

小于 `1` 为缩小

大于 `1` 为放大





## 缩放 scale()

> transform: scale()

该位移方法设置在 `transform` 上

根据需要设置在正确的位置上



**语法:**

```css
/* 设置 x 轴缩放 */
transform: scaleX(2);

/* 设置 y 轴缩放 */
transform: scaleY(0.5);

/* 设置 z 轴缩放 */
transform: scaleZ(1.5);

/* 同时设置 x 和 y 轴缩放*/
transform: scale(2);

/* 分别设置 x 和 y 轴缩放*/
transform: scale(2, 1.5);

/* 分别设置 x 和 y 和 z 轴缩放*/
transform: scale3d(2.5, 1.2, 0.3);
```



*注意:*

缩放设置直接填写缩放的比例 

正常大小为 `1` 

小于 `1` 为缩小

大于 `1` 为放大





## 倾斜 skew()

> transform: skew()

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-function/skew" target="_blank">MDN文档</a> 

倾斜也被称为斜切 , 倾斜的单位采用度数 , 通过该方法可以对一个元素进行倾斜变换

这种转换是一种剪切映射 (横切)，它在水平和垂直方向上将单元内的每个点扭曲一定的角度 . 

每个点的坐标根据指定的角度以及到原点的距离，进行成比例的值调整；因此，一个点离原点越远，其增加的值就越大 . 

`skew()` 函数指定一个或两个参数，它们表示在每个方向上应用的倾斜量



**语法:**

```css
/* 对 x 轴倾斜*/
transform: skewX(30deg);

/* 对 y 轴倾斜*/
transform: skewY(1.07rad);

/* 对 x 和 y 轴进行倾斜*/
transform: skew(30deg, 20deg);
```





## 矩阵 matrix()

> transform: matrix()

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-function/matrix" target="_blank">MDN文档</a> 

CSS 函数 `matrix()` 指定了一个由指定的 6 个值组成的 2D 变换矩阵。这种矩阵的常量值是隐含的，而不是由参数传递的；其他的参数是以列优先的顺序描述的



**语法:**

```css
transform: matrix(1.0, 2.0, 3.0, 4.0, 5.0, 6.0);

transform: matrix3d(1.0, 2.0, 3.0, 4.0, 5.0, 6.0, 7.0, 8.0, 9.0, 10.0, 11.0, 12.0, 13.0, 14.0, 15.0, 16.0);
```



*注意:*

矩阵实际就是其他变换方法的另一种形式





## 设置景深 perspective

> perspective

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/perspective" target="_blank">MDN文档</a> 

景深也被称为观察者视角



**语法:**

```css
 perspective: <length>;
```



*注意:*

通常该属性配合需要进行3d变换的css方法使用

景深的数值通常设置在 800px 至 1500px 之间





## 设置变换点 transform-origin

> transform-origin

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-origin" target="_blank">MDN文档</a> 

**`transform-origin`** CSS 属性让你更改一个元素变形的原点, 默认的转换原点是 `center`



**语法:**

```css
/* 设置 x 轴变换点*/
transform-origin: center;

/* 设置 x 和 y 轴变换点*/
transform-origin: left top;

/* 设置 x 和 y 和 z 轴变换点*/
transform-origin: left top -50px;
```



- 一个值：必须是 \<length>，或 left, center, right, top, bottom 关键字中的一个。
- 两个值：其中一个必须是 \<length>，或 left, center, right 关键字中的一个。另一个必须是 \<length>，或 top, center, bottom 关键字中的一个。
- 三个值：前两个值和只有两个值时的用法相同。第三个值必须是 \<length>。它始终代表 Z 轴偏移量。



*注意:*

\<length> 表示 css 中接收的单位, 如 px % rem 等等





## 设置变换空间 transform-style

> transform-style

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/transform-style" target="_blank">MDN文档</a> 

通过该属性可以设置一个元素是位于 2d空间 或者 3d空间中



**语法:**

```css
/* 2d空间 默认值 */
transform-style: flat;

/* 3d空间 */
transform-style: preserve-3d;
```



*注意:*

通常该属性配合需要进行3d变换的css方法使用





## 设置观察者视角是否可见 backface-visibility

> backface-visibility

**`backface-visibility`** 指定当元素背面朝向观察者时是否可见

元素的背面是其正面的镜像。虽然在 2D 中不可见，但是当变换导致元素在 3D 空间中旋转时，背面可以变得可见。 （此属性对 2D 变换没有影响，它没有透视。）



**语法:**

```css
/* 背面朝向用户时可见 默认值 */
backface-visibility: visible;

/* 背面朝向用户时不可见 */
backface-visibility: hidden;
```



*注意:*

该属性通常配合一些旋转元素使用
