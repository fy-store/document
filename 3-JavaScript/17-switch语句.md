## switch语句

> switch语句也是循环的一种



**示例:**

```js
switch(2) {
	case 1:
  		console.log("a");
  		break;
	case 2:
  		console.log("b");
  		break;
	case 3:
  		console.log("c");
  		break;
	default:
  		console.log('所有都不匹配时输出');
  		break;
}
```



**swich 语句解析:**

- 若 case 判断第一个成功，尽管不在判断后面的 case 语句
- 但其依然会执行后面 case 里的内容（下漏，机械执行）
- 所以为了消除这种效果会在 case 语句最后加上 break 进行终止
- case 使用严格比较（===）类型和值必须与要匹配的类型和值相同。
  - case 中书写表达式, 为 `true` 则执行代码体, 为 `false` 则不执行



**break:**

- break 终止语句, 终止循环（跳出循环）
- break 只能放在 switch 和循环里(for, while, for in)，否则会报错



**continue:**

- 终止本次循环，进行下一次循环 (即跳过本次循环) , 使用方法同 break



**default:**

- default 所有的 case 都不匹配时执行 一般放在最后





## 循环中使用break和continue

```js
for(var i = 0; i < 10; i++) {
    if(i === 5) {
        continue
    }
}

// -------------

var num = 0;
while(1) {
    num++
    if(num === 10) {
        break
    }
}
```

