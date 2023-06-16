## css 选择器

> <a href="https://developer.mozilla.org/zh-CN/docs/Learn/CSS/Building_blocks/Selectors" target="_blank">MDN文档</a>
>
> 以下为常用的选择器和使用方式



### * 通配符选择器

> 通配符选择器
>
> 使用 `*` ，选择所有元素

```css
* {}
```



### 元素选择器

> 选中特定的元素
>
> 使用 元素标签名

```css
span {}
```



### id 选择器

> id 选择器
>
> 使用 #

```css
#app {}
```



### class 选择器

> class 选择器
>
> 使用 .

```css
.container {}
```



### 属性选择器

> 属性选中元素，或者选中一个元素并添加属性或再添加值以达到限制选中范围

更多使用方法：<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/Attribute_selectors" target="_blank">MDN文档</a> 

```css
/** 属性选择 **/
[href="https://www.rgbcode.cn"]{}
#app[data-test] {}

/** 属性值等于该值 **/
#app[data-test="test"] {}

/** 以其开头 **/
#app[data-test^="t"] {}

/** 以其结尾 **/
#app[data-test$="t"] {}

/** 包含 **/
#app[data-test*="t"] {}

/** 等等 **/
```



### 伪类选择器

> 伪类 <a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/Pseudo-classes" target="_blank">MDN文档</a> 



#### 伪类状态

> 选中某些元素的某种状态
>
> 使用时需注意顺序，link > visited > hover > active

- link 超链接未访问时的状态
- visited 超链接访问过后的状态
- hover 鼠标悬停状态
- active 激活状态，鼠标按下的状态(当元素被点击时)

```css
#app:hover {}
#app:hover .container {}
```



#### 表单类伪类

> :focus
>
> 选择元素聚焦时

> :disabled
>
> 元素被禁用时

> :checked
>
> 单选或多选框被选中时

等等... 这类伪类使用较少



#### :first-child

> 选中第一个元素且它在其父级内排列必须是第一个子元素

```css
#app div:first-child{}
```



#### :first-of-type

> 选中第一个指定的元素，而不考虑它在其父级下排列是否为第一个子元素

```css
#app .item:first-of-type{}
```



#### :last-child

> 选中最后一个元素且它在其父级内排列必须是最后一个子元素

```css
#app div:last-child{}
```



#### :last-of-type

> 选中最后一个指定的元素，而不考虑它在其父级下排列是否为最后一个子元素

```css
#app .item:last-of-type{}
```



#### :nth-child(n)

> 选中第 n 个元素，且它在其父级内排列必须是第n个子元素
>
> 注意点：

- n 其中 0 开始计算
- even 关键词 等同于 2n
- odd  关键字 等同于 2n+1

```css
#app div:nth-child(-n + 3) {} /* 选中前三个元素 */
```



#### :nth-of-type(n)

> 选中第 n 个元素，而不考虑它在其父级下排列是否为第n个子元素

```css
#app .item:nth-of-type(n)(-n + 3) {} 
```



### 伪元素选择器

> 伪元素选择器可以使用一个 : 因为浏览器会为我们再补上一个



#### ::before 和 ::after

> before 和 after
>
> 关于伪元素
>
> 伪元素天生就是行盒，伪元素不会创建实际dom
>
> ::before 和 ::after的所在位置：`<span>before 哈哈哈 after</span>`
>
> 属性 content 是必须的，否则 ::before 和 ::after 无法生效

```css
#app::before {
    content: "可以写文本";
}

#app::after {
    content: "也可以留空";
}
```



#### ::first-letter

> 选中元素中的第一个字母

```css
#app::first-letter {}
```



#### ::first-line

> 选中元素中的第一行文字

```css
#app::first-line {}
```



#### ::selection

> 选中被用户框选的文字

```css
#app::selection {}
```