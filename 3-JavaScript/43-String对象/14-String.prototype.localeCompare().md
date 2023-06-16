## String.prototype.localeCompare()

该方法使用本地的字典语言来进行比较字符串的大小

可以通过这个方法来完成字典排序



**语法:**

```js
str.localeCompare(compareString [, locales] [, options])
```



- `compareString`

  要比较的字符

- `locales` [可选]

  使用比较的语言

- `options`

  配置对象 , 详情参考文档



**返回值:**

如果引用字符串（`referenceStr`）存在于比较字符串（`compareString`）之前则为**负数**；如果引用字符串存在于比较字符串之后则为**正数**；相等的时候返回 `0`。

​	

**示例:**

*字典排序*

```js
const arr = ['广州', '深圳', '上海', '杭州', '北京']
const result = arr.sort((a, b) => a.localeCompare(b))
console.log(result) // ['北京', '广州', '杭州', '上海', '深圳']
```

