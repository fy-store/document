## String.prototype.at()

该方法用于取字符串中的第几位 , 和通过下标取字符一样 , 区别就是该方法支持用负数来取倒数位 .

该方法允许正整数和负整数 . 



**语法:**

```js
str.at(index)
```



- `index`

  要取的字符的下标



**返回值:**

指定的字符



**例如:**

在以前我们想取最后一位字符

```js
var str = 'abc'
var result = str[str.length - 1]
console.log(result) // c
```



**at() 方法:**

```js
var str = 'abc'
var result = str.at(-1)
console.log(result) // c
```

