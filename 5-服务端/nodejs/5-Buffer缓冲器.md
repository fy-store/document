## Buffer 缓冲器

> 用于储存数据，图片数据，音频视频数据等等

数据到 Buffer 手中时将被转成二进制数据 1010101...

1.Buffer 是一个类似数组的对象，用于存储数据，存储的是二进制数据

2.Buffer 的效率很高，存储数据很快，它是直接对计算机的内存进行操作

3.Buffer 的大小一旦确定了，不可修改

4.每个元素占用内存的大小为1字节

5.Buffer 是 node 中非常重要的内置核心模块，其在 global 上，可以直接使用 

6.输出的（展示） Buffer 将以16进制方式展示


### new Buffer()

> 该方法已废弃



### Buffer.alloc()

> 创建一个Buffer
>
> 该方法创建Buffer后会进行初始化

语法：`Buffer.alloc(size[, fill[, encoding]])`

- size：\<integer> 新建的 `Buffer` 期望的长度
- fill：\<string> | \<buffer> | \<integer> 用来预填充新建的 `Buffer` 的值。 **默认:** `0`
- encoding：\<string> 是字符串，则该值是它的字符编码。 **默认:** `'utf8'` 

分配一个大小为 `size` 字节的新建的 `Buffer` 。 如果 `fill` 为 `undefined` ，则该 `Buffer` 会用 **0 填充**。

```js
const buf = Buffer.alloc(5);

console.log(buf); // 输出: <Buffer 00 00 00 00 00>
```



### Buffer.allocUnsafe()

> 创建一个Buffer
>
> 该方法创建Buffer后不会进行初始化，速度会比 `Buffer.alloc` 稍快
>
> 但是由于未进行初始化，可能会存在上一次使用该空间的残余数据，存在一定安全隐患

语法：`Buffer.allocUnsafe(size)`

- size：\<integer> 新建的 `Buffer` 期望的长度

```js
const buf = Buffer.allocUnsafe(10);

console.log(buf); // 输出: (内容可能不同): <Buffer a0 8b 28 3f 01 00 00 00 50 32>

buf.fill(0); // 初始化填充 0

console.log(buf); // 输出: <Buffer 00 00 00 00 00 00 00 00 00 00>
```



### Buffer.from()

> 创建一个Buffer流
>
> 将数据存入一个 Buffer 中，不指定 Buffer 的大小，类似写入流

语法：`Buffer.from(array)`

- array：\<Array> 通过一个八位字节的 `array` 创建一个新的 `Buffer` 。

```js
// 创建一个新的包含字符串 'buffer' 的 UTF-8 字节的 Buffer
const buf = Buffer.from([0x62, 0x75, 0x66, 0x66, 0x65, 0x72]);
```



语法：`Buffer.from(arrayBuffer[, byteOffset[, length]])`

- arrayBuffer：*\<ArrayBuffer>* | *\<SharedArrayBuffer>* ArrayBuffer 或 SharedArrayBuffer 或 TypedArray 的 .buffer 属性。
- byteOffset： \<integer> 开始拷贝的索引。默认为 `0`。
- length：\<integer> 拷贝的字节数。默认为 `arrayBuffer.length - byteOffset`。

该方法将创建一个 ArrayBuffer 的视图，而不会复制底层内存。例如，当传入一个 TypedArray 实例的 .buffer 属性的引用时，这个新建的 Buffer 会像 TypedArray 那样共享同一分配的内存。

可选的 `byteOffset` 和 `length` 参数指定将与 `Buffer` 共享的 `arrayBuffer` 的内存范围。

```js
const arr = new Uint16Array(2);

arr[0] = 5000;
arr[1] = 4000;

const buf = Buffer.from(arr.buffer); // 与 `arr` 共享内存

console.log(buf); // 输出: <Buffer 88 13 a0 0f>

arr[1] = 6000; // 改变原始的 Uint16Array 也会改变 Buffer

console.log(buf); // 输出: <Buffer 88 13 70 17>
```



语法：`Buffer.from(buffer)`

```js
const buf1 = Buffer.from('buffer');
const buf2 = Buffer.from(buf1);

buf1[0] = 0x61;

// 输出: auffer
console.log(buf1.toString());

// 输出: buffer
console.log(buf2.toString());
```



语法：`Buffer.from(string[, encoding])`

- string： \<string> 要编码的字符串
- encoding：\<string>  `string` 的字符编码。 **默认:** `'utf8'`

新建一个包含所给的 JavaScript 字符串 `string` 的 `Buffer` 。 `encoding` 参数指定 `string` 的字符编码。

```js
const buf1 = Buffer.from('this is a tést');

// 输出: this is a tést
console.log(buf1.toString());

// 输出: this is a tC)st
console.log(buf1.toString('ascii'));


const buf2 = Buffer.from('7468697320697320612074c3a97374', 'hex');

// 输出: this is a tést
console.log(buf2.toString());
```



Buffer 存的是二进制数据，但是展示的是16进制数据，有一些数据可以在调用 toString() 方法转回原始数据

例如字符串，而音频视频等的则不可

```js
let buf4 = Buffer.from('hello');
console.log(buf4);
console.log(buf4.toString());
```



### Buffer.isBuffer(obj)

> 判断是否为Buffer，返回一个Boolean



### 待补充

