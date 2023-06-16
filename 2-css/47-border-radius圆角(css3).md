## border-radius 圆角 (css3)

> border-radius

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/border-radius" target="_blank">MDN文档</a> 

这是一个简写属性，具体属性：

- border-top-left-radius
- border-top-right-radius
- border-bottom-right-radius
- border-bottom-left-radius

使用：

border-radius: 数值; 圆角

原理：

  多大值即做多大半径，后画出一个圆并将圆与角相交多余的去掉

简写：

  border-radius: 10px 20px 30px 40px;

  一个值：四个角

  两个值：左上右下，右上左下

  三个值：左上，右上左下，右下

  四个值：左上，右上，右下，左下

圆形：

  通常设置为 50%

设置不规则圆：

  最多可以设置8个值

  border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;

如果在斜杠之前和之后给出值，则斜杠前面的值设置水平半径，

斜杠后面的值设置垂直半径。如果没有斜杠，则值将两个半径均等地设置。