## css 全局属性 all

> all

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/all" target="_blank">MDN文档</a> 

`all` 是一个简写属性, `all` 将除了 `unicode-bidi` 与 `direction` 之外的所有属性重设至其初始值，或继承值, 所以可以把它认为是一个全局属性

`all` 所应用的属性都是针对父元素的, 并非包含块 .



**all 的具体属性:**

- `initial` 初始值，实现使用该值的元素将重置为初始值

- `inherit` 应用父元素的属性，<del>属性使用该值将强制继承父级</del>, 此继承并非属性计算值计算过程中的继承, 该属性表示将父元素的该属性复制一份放到此处
- `unset` 如果该元素的属性的值是可继承的，则应用其父元素的值(在属性值计算的前两步中进行操作, 使其避开第三步的继承)，反之则改变为初始值。

- `revert` 指定依赖于声明所属的样式表原点的行为, 详情查阅文档



**示例:**

*应用父元素的所有属性*

应用了父元素的所有属性后还可再设置属性进行覆盖

```html
<div class="box">
    <div class="child"></div>
</div>
```

```css
.box {
    width: 300px;
    height: 300px;
    background-color: red;
}

.child {
    all: inherit;
    width: 200px;
    background-color: green;
}
```



*指定应用父元素一个属性的值*

```css
color: inherit;
```



*重置为初始值*

```css
margin: initial;
```

