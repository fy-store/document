## web字体和图标

> web字体和图标

<a href="https://developer.mozilla.org/zh-CN/docs/Web/CSS/@font-face" target="_blank">MDN文档</a> 

- web字体：

  用户电脑上没有安装相应字体，强制让用户下载该字体

  使用 @font-face 指令制作一个新字体

```css
@font-face {
  font-family: "自己定义名字";
  src: url("字体的文件路径");
}

p {
  font-family: "填写自己定义的名字";
}
```



- 字体图标

​		iconfont.cn 阿里图库