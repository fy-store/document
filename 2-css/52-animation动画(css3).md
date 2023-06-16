## @keyframes css3

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/@keyframes" target="_blank">MDN文档</a> 

`@keyframes` 用于定义动画的关键帧

关键帧中可以通过关键字 `from` 和 `to` 分别指定动画开始状态和结束状态

***示例:***

```css
@keyframes opcity {
    from {
		opcity: 0;
    }
    
    to {
        opcity: 1;
    }
}
```



关键帧除了通过关键字指定外还可通过百分比指定更加细致的关键帧

***示例:***

```css
@keyframes opcity {
    0% {
        opcity: 0;
    }
    
    30%, 50% {
        opcity: 1;
    }
    
    100% {
        opcity: 0;
    }
}
```



**注意:**

如果在关键帧的样式中使用了不能用作动画的属性，那么这些属性会被忽略掉，支持动画的属性仍然是有效的，不受波及 .

关键帧中出现的 `!important` 将会被忽略 .



## animation 动画 css3

> animation

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/animation-name" target="_blank">MDN文档</a> 

`animation` 是一个简写属性, 它可以用来制作网页中的动画效果 .



**简写使用语法:**

```css
animation: [使用的动画] [动画运行时长] [动画运行前的等待时长] [动画运动曲线] [动画运行次数] [动画是否反复播放] [动画开始或最后的应用样式] [动画是否播放];

/* 使用多个动画 */
animation: [使用的动画] [动画运行时长] [动画运行前的等待时长] [动画运动曲线] [动画运行次数] [动画是否反复播放] [动画开始或最后的应用样式] [动画是否播放],
		   [使用的动画] [动画运行时长] [动画运行前的等待时长] [动画运动曲线] [动画运行次数] [动画是否反复播放] [动画开始或最后的应用样式] [动画是否播放],
		   [使用的动画] [动画运行时长] [动画运行前的等待时长] [动画运动曲线] [动画运行次数] [动画是否反复播放] [动画开始或最后的应用样式] [动画是否播放];
```



*示例:*

```css
@keyframes opcity {
    from {
        opcity: 0;
    }
    
    to  {
        opcity: 1;
	}
}

.opcity {
    animation: opcity 3s linear forwards;
}
```





**animation 具体属性:**

- `animation-name`  指定需要使用的动画

  - 语法: animation-name: name1 [, name2 ...];

  

- `animation-duration` 指定动画周期的时长

  - 语法: animation-duration: \<name1-time> [, \<name2-time> ...];
  - 示例: animation-duration: 2s, 500ms;
  - 默认值: 0s 表示无动画

  

- `animation-timing-function` 设置动画的运动速度曲线

  - linear 匀速


  - ease 默认。动画以低速开始，然后加快，在结束前变慢。

  - ease-in 动画以低速开始。

  - ease-out 动画以低速结束。

  - ease-in-out 动画以低速开始和结束。

  - cubic-bezier(n,n,n,n) 设置贝塞尔曲线, 在 cubic-bezier 函数中自己的值, 可能的值是从 0 到 1 的数值。
  - steps(num [, 动画运动速度函数]) 指定了时间函数中的间隔数量（步长）填数字, 应用于奔跑的动画等, 似动画一帧一步播放效果(电影胶卷)
  - 语法: \<name1-timing-function> [, \<name2-timing-function> ...];

  

- `animation-delay` 设置动画开始前的等待时长(动画的延迟时间)

  - 默认为 0s .
  - 定义一个负值会让动画立即开始。但是动画会从它的动画序列中某位置开始 . 例如，如果设定值为 -1s，动画会从它的动画序列的第 1 秒位置处立即开始 .
  - 语法: animation-delay: \<name1-delay> [, \<name1-delay> ...];

  

- `animation-iteration-count` 规定动画的运行次数

  - 语法: animation-iteration-count: \<name1-num1> [, \<name2-num2> ...];
  - 值是一个数值, 可以是小数, 例如 1.5 那么第二次将播放到一半, 不可为负值 .
  - 示例: animation-iteration-count: 2, 1.7, 1.5;
  - 可使用关键字: infinite , 表示无限循环播放动画 . 

  

- `animation-direction` 指示动画是否反向播放

  - normal 默认值, 动画重新播放时从初始位置重新开始
  - alternate 动画交替反向运行
  - reverse 反向运行动画, 每周期结束动画由尾到头运行 *[常用]*
  - alternate-reverse 反向交替，反向开始交替
  - 语法: animation-direction: \<name1-direction> [,\<name2-direction> ...];

  

- `animation-fill-mode` 设置动画在执行之前和之后如何将样式应用于其目标

  - none 默认值, 动画执行时赋予相应关键帧中的样式
  - forwards 动画结束时样式停留在最后一个关键帧 [*常用*]
  - backwards 动画将在应用于目标时立即应用第一个关键帧中定义的值，并在animation-delay期间保留此值
  - both 动画将遵循forwards和backwards的规则，从而在两个方向上扩展动画属性。
  - 语法:  animation-fill-mode: \<name1-fill-mode> [,\<name2-fill-mode> ...];

  

- `animation-play-state` 定义一个动画是否运行或者暂停
  - running 当前动画正在运行
  - paused 当前动画已被停止
  - 可以通过 js 操作动画该属性来达到 暂停 和 继续 动画
  - 语法: animation-play-state: \<name1-play-state> [,\<name2-play-state> ...];

