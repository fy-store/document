## Number.isNaN()

`Number.isNaN()` 方法确定传递的值是否为 `NaN`，并且检查其类型是否为 `Number` 。

它是原来的全局 `isNaN()` 的更稳妥的版本。

全局的 `isNaN()` 先将数据转为数字类型 , 转换后只要是 `NaN` 都将被判定为 `NaN` 

这显然不是我们所要的结果 , 我们希望的是直接判断是否为 `NaN` 而非将数据进一步转换 .



**语法:**

```js
Number.isNaN(value)
```



- `value`  

  要检测的数据



**返回值:**

布尔值 , 是 NaN 返回 true , 不是 NaN 返回 false



**全局版本**

```js
isNaN('123') // false
isNaN('abc') // true
isNaN(NaN) // true
```



**Number.isNaN()**

```js
Number.isNaN('123') // false
Number.isNaN('abc') // false
Number.isNaN(NaN) // true
```



