## Array.prototype.sort()

对数组进行排序 , 该方法改变原数组 .



**语法:**

```js
arr.sort([compareFn])
```



- `compareFn`

  处理函数 , 接受两个参数 , a 和 b , 根据该函数的返回值来决定 a 和 b 是否调换位置 .

  - `a`

    第一个用于比较的元素

  - `b`

    第二个用于比较的元素



如果省略该函数，数组元素会被转换为字符串，然后根据每个字符的 Unicode 码点值进行排序 . 



**返回值:**

一个排序后的数组 . 



**指示:**

- 当返回值为负数时，那么前面的数放在前面(a在前, b在后)
- 当返回值为正数时，那么后面的数在前(a和b调换顺序 , b在前 , a在后)
- 当返回值为 0 时，那么不进行变动
- 升序 return a - b;
- 降序：return b - a;
- 乱序：return Math.random() - 0.5;
- 该方法改变原数组，并且返回值是改变后的数组



**示例:**

*示例1*

升序

```js
var arr = [1, 3, -2, -5, 5, 5, 10, 8, 4]
arr.sort(function (a, b) {
    return a - b
})
console.log(arr) // [-5, -2, 1, 3, 4, 5, 5, 8, 10]
```



*示例2*

```js
arr.sort(function (a, b) {
  // 升序
  // if (a > b) {
  //     return 1;
  // }else {
  //     return -1;
  // }

  // 简化升序
  return a - b;

  // 降序
  // if (a < b) {
  //     return 1;
  // }else {
  //     return -1;
  // }

  // 简化降序
  // return -(a - b);
  // 再简化
  // return b - a;

    // 乱序
  // return Math.random() - 0.5;
})
```

