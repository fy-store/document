## 引言

JavaScript（JS）是一种具有函数优先特性的轻量级、解释型或者说即时编译型的编程语言。

JavaScript 是一种基于原型、多范式、单线程的动态语言，并且支持面向对象、命令式和声明式（如函数式编程）风格。



## 页面中引入js

> 本节内容推荐 《JavaScript 高级程序设计》4

使用 `script` 元素引入js , 由于页面解析 js 时将会阻塞页面 , 所以我们通常将 `script` 放置在body元素内的最尾部(body元素结束标记之前)

*示例:*

```html
<html>
    <body>
        <h1></h1>
        <div></div>
    	<script src=""></script>
    </body>
</html>
```



**js两种使用方式:**

- 页面js , 在 `script` 元素内直接书写js代码
- 外部js , 单独创建一个js文件书写js , 随后通过 `script` 元素上的 `src` 书写引入js , 外部js文件的后缀通常为 .js



*注意:*

若采用外部js , 那么 `script` 元素内将不能在书写js, 即使书写了也会被忽略 .

为了便于维护和管理 , 我们通常使用外部js方式



**script的书写位置:**

虽说我们通常将 `script` 元素放置在body内的最尾 , 但这不是必须的 .

因为执行js时会对页面造成阻塞 , 所以 `script` 元素放置其他位置时我们通常会进行而外的处理, 延迟其执行



*DOMContentLoaded事件:*

如果需要放将 `script` 放置在其他位置 如 head 中, 那么其内部的js应放置在 `DOMContentLoaded` 事件的回调中

`DOMContentLoaded` 事件将会在dom解析完后触发 , 需注意不要和 `load` 事件搞混

window 上的 `load` 事件会在页面所有资源加载完毕后才触发, 如果页面中有一个资源加载失败那么该事件便不会触发



*正确的示例:*

```html
<html>
    <head>
    	<script>
        	 document.addEventListener('DOMContentLoaded', function () {});
        </script>
    </head>
    <body>
        <h1></h1>
        <div></div>
    </body>
</html>
```



*MDN:*

 https://developer.mozilla.org/zh-CN/docs/Web/API/Document/DOMContentLoaded_event



**动态加载外部js:**

创建script，插入到dom中，加载完毕后 callBack。

可达到兼容, 可以按需加载, 实际是利用 html 加载外部资源异步的方法



*示例:*

```html
var script = document.createElement('script');
script.src = 'xxx.js'; // 当读到这一句时就会开始加载 (异步加载)
script.async = false;
script.onload = function () {
  // 当它下载完后才执行load事件的回调
}
document.body.appendChild(script); // 当将dom插入到页面时才开始执行
```





**另外的异步加载方案:**

*script元素上的async属性:*

该属性只对外部js生效 .

该属性是一个布尔属性 , 若添加了该属性那么该 `script` 所引入的js代码不会立即执行

使用 `async` 后, 当解析器读取到该 `script` 元素时会对其资源进行异步加载, 但不执行, 所以不会阻塞页面

在 DOM 加载后执行 , 但该执行不保证脚本的执行顺序 , 所以使用该属性的重点是对其他 `script` 没有依赖关系



*script元素上的defer属性*

可以外部链接或者也可以将代码写到script内部

等到dom文档全部解析完才会被执行 , 在 `DOMContentLoaded` 事件触发之前



*示例:*

```html
<script src='' async='async'></script> 
<script src='' defer='defer'></script> 
```





## script元素的其他属性

除 `src` [可选] 外, script 上还有很多属性, 其中便有一个属性 `type` [可选]

`type` 在之前被用于指定脚本语言内容类型(MIME) , 起初是为了支持其他脚本语言嵌入到浏览器中 , 不过至今我们已经不再需要了 , 现如今浏览器中默认只支持 JavaScript 脚本语言

`type` 还有另外一个作用, 当其值为 `module` 时, 浏览器将会把该 script 作为一个模块(后面es6模块化的知识)



还有一些其他属性 , 但已不再重要
