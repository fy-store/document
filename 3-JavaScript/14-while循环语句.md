## while循环语句

`while` 判断表达式, 为 `true` 则执行循环体, 为 `false` 则终止循环



**语法:**

```js
while(表达式) {
    // code...
}
```





**示例:**

```js
var num = 0;
while(num < 10) {
    num++
}
```



*无限循环*

```js
while(1) {
    // code...
}
```

此时便成了死循环, 可以在循环体内通过判断使用 break 来进行跳出循环

表达式转为布尔值为 `true` 即可, 并非一定为 1