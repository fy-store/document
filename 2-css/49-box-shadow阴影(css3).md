## box-shadow 阴影 css3

> box-shadow

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/box-shadow"
        target="_blank">MDN文档</a> 

通过 `box-shadow` 可以设置盒子的阴影, 通过盒子阴影可以展示出很多视觉效果



**语法:**

```css
box-shadow: x轴偏移量 y轴偏移量 [模糊半径] [扩散半径] [阴影颜色] [inset];
```



**参数:**

`inset` 该关键字为可选值, 若不填写默认为外阴影, 若填写该关键字将变为内阴影

模糊半径, 值越大，模糊面积越大，阴影就越大越淡, 不能为负值。默认为 0

扩散半径, 取正值时，阴影扩大；取负值时，阴影收缩。默认为 0



**示例:**

```css
box-shadow: 10px 10px 6px #ccc;
```



**设置多个阴影:**

阴影是可以设置多个的, 使用逗号进行分割

```css
box-shadow: 10px 10px 6px #ccc,
			5px 5px 3px #ddd
			2px 2px 5px #000;
```

