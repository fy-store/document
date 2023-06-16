## Object.defineProperty()

> 描述对象属性

<a href="https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty" target="_blank">MDN文档</a> 



**语法:**

```js
Object.defineProperty(obj, prop, descriptor)
```



**参数:**

- `obj`

要定义属性的对象



- `prop`

要定义或修改的属性的名称或 `Symbol` 



- `descriptor`

要定义或修改的属性描述符(配置对象)



**配置对象的参数:**

*数据描述符*

- `configurable` 

配置参数是否允许被修改, `true` / `false`

当且仅当该属性的 `configurable` 键值为 `true` 时，该属性的描述符才能够被改变，同时该属性也能从对应的对象上被删除。 **默认为** **`false`**



- `enumerable`

是否允许被枚举, `true` / `false` ,  **默认为** **`false`**



- `value`

该属性对应的值, 可以是任何有效的 JavaScript 值（数值，对象，函数等）, **默认为 `undefined`**。



- `writable`

配置对象中的 `value` 属性是否允许被更改, `true` / `false` ,  **默认为** **`false`**



*存取描述符*

- `get`

属性的 getter 函数，如果没有 getter，则为 `undefined`。当访问该属性时，会调用此函数。执行时不传入任何参数，但是会传入 `this` 对象（由于继承关系，这里的`this`并不一定是定义该属性的对象）。该函数的返回值会被用作属性的值。 **默认为 `undefined`**。



- `set`

属性的 setter 函数，如果没有 setter，则为 `undefined`。当属性值被修改时，会调用此函数。该方法接受一个参数（也就是被赋予的新值），会传入赋值时的 `this` 对象。 **默认为 `undefined`**。





**返回值:**

被传递给函数的对象



**<span style="color:#f00;">注意:</span>**

如果一个描述符不具有 `value`、`writable`、`get` 和 `set` 中的任意一个键，那么它将被认为是一个数据描述符。如果一个描述符同时拥有 `value` 或 `writable` 和 `get` 或 `set` 键，则会产生一个异常。