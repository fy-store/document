## for-in循环语句

`for-in` 语句通常用于枚举对象, 当然数组和字符串也是可以的



**示例:**

```js
var obj = {
    name: '小明',
    age: 19
}

for(var k in obj) {
    // 键
    console.log('键', k);
    
    // 值
    console.log('值', obj[k]);
}
```



**小知识:**

对象在取值时可通过 `.` 的方式, 也可以通过 `[]` 的方式进行取值 .

```js
var obj = {
    name: '小白'
}

obj.name // 小白
obj['name'] // 小白
```



 此时便可通过 `[]` 使用变量的方式来取特定的值

```js
var obj = {
    name: '小白'
}

var x = 'name'
obj[x] // 小白
```



实际上很容易理解, 想想数组的取值便可



