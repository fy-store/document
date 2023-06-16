## transition 过渡 css3

> transition

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/transition"
        target="_blank">MDN文档</a> 

`transition` 过渡, 使用该属性可以过渡对数值类的css属性进行过渡

需要注意的是 `transition` 只能针对数值变化这种属性进行过渡, 如 `height` `color` `option` 等

而不具备数值的属性将无法过渡, 如 `display:node` 变成 `display:block` , 由于不是数值的变化所以无过渡效果

`transition` 是一个简写属性



**简写使用语法:**

```css
transition: 过渡的属性或关键字 过渡的时长 [过渡的88速度曲线] [过渡前等待的时间];

/* 使用多个过渡 */
transition: 过渡的属性或关键字 过渡的时长 [过渡的速度曲线] [过渡前等待的时间],
			过渡的属性或关键字 过渡的时长 [过渡的速度曲线] [过渡前等待的时间],
			过渡的属性或关键字 过渡的时长 [过渡的速度曲线] [过渡前等待的时间];
```



**示例:**

```css
transition: height .5s linear;
```





**具体属性为:** 

-  `transition-property`  指定应用过渡属性的名称

  - 关键字取值: `none` 无过渡
  - 关键字取值: `all` 所有属性都被过渡
  - 过渡 `具体` 的属性, 如 `background-color` 或 直接对整个 `background` 进行过渡
  - 可以指定过渡多个属性, 如  `transition-property: color, height, all;`

  

- `transition-duration` 过渡的时长

  - 取值单位 `s` 秒 , `ms` 毫秒, 默认值为 `0s`
  - 可以指定针对多个过渡应用的过渡时长, 与 *transition-property* 列表一一对应

  

- `transition-timing-function` 过渡的方式(过渡的速度曲线)

  - ease 逐渐慢下来(默认值)
  - linear 匀速 
  - ease-in 加速
  - ease-out 减速
  - ease-in-out 先加速后减速
  - steps() 步长(后续再了解)
  - 或使用自定义 *贝塞尔曲线*
  - 可以指定针对多个过渡应用的过渡速度曲线, 与 *transition-property* 列表一一对应

  

- `transition-delay` 过渡前等待时间

  - 取值单位 `s` 秒 , `ms` 毫秒, 默认值为 `0s`
  - 可以指定针对多个过渡应用的过渡前等待时间, 与 *transition-property* 列表一一对应

