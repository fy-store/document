##  File system 文件系统

> 模块命名 fs ，需要引入

引入 fs 模块

```js
const fs = require('fs')
```





### 文件系统的事件

> 绑定事件使用 on(event) 函数

- `'open'` 文件流打开时触发

- `'close'` 文件底层流或资源被关闭时触发，不是所有可写流都会触发 `'close'` 事件

- `'error'` 事件在读写数据出错或者使用管道出错时触发，回调函数会接受到一个 error 参数

- 待补充





### 相对转绝对路径

> 异步的将相对路径转为绝对路径

语法：`fs.realpath(path[, options], callback)`

- path：*\<string> | \<buffer> | \<url>* 要解析的目录/文件
- options：*\<string> | \<object>* 配置参数
  - encoding： *\<string>* 默认值 utf-8
- callback：*\<function>* 回调函数
  - error：错误
  - resolvedPath：转换后的结果

```js
fs.realpath('./item1/file.txt', (err, path) => {
    if (err) {
        console.log('错误');
    } else {
        console.log('成功');
        console.log(path);
    }
})
```





### 拷贝一个文件

> 异步拷贝一个文件到另一处

语法：`fs.copyFile(src, dest[, flags], callback)`

- src：*\<string> | \<buffer> | \<url>* 要被拷贝的源文件名称

- dest：*\<string> | \<buffer> | \<url>* 拷贝操作的目标文件名
- flags：*\<number>* 拷贝操作修饰符，是一个可选的整数，用于指定行为的拷贝操作 *默认:* `0`

- callback：*\<function>* 回调，失败将传入一个 *error* 参数

> 如果拷贝目标已存在则将会被覆盖。

```js
fs.copyFile('./item1/file.txt', './item2/new_file.txt', (err) => {
    if(err) {
        console.log('拷贝失败');
    }else {
        console.log('拷贝成功');
    }
})
```





### 创建一个文件夹

> 异步创建目录

语法：`fs.mkdir(path[, mode], callback)`

- path：*\<string> | \<buffer> | \<url>* 创建的路径

- mode：*\<integer>* 设置文件的操作权限，默认为 0o777（8进制）

  0o666 = 0o222 + 0o444 即可读可写，书写时直接写8进制，勿写字符串

  - 0o111 文件可被执行的权限 .exe 等
  - 0o222 文件可被写入的权限
  - 0o444 文件可被读取的权限

- callback：*\<function>* 失败将传入一个 error 参数

```js
fs.mkdir('./item3/demo', (err) => {
    if (err) {
        console.log('error');
    } else {
        console.log('成功');
    }
})
```





### 重命名文件夹/文件

> 异步的重命名文件夹/文件并移动到新的位置

语法：`fs.rename(oldPath, newPath, callback)`

- oldPath：*\<string> | \<buffer> | \<url>* 需要更改的文件
- newPath：*\<string> | \<buffer> | \<url>* 新的位置+名字
- callback：*\<function>* 失败将传入一个 error 参数

```js
fs.rename('./item1/file.txt', './item2/new_name.txt', (err) => {
    if (err) {
        console.log('错误');
    } else {
        console.log('成功');
    }
})
```





### 删除一个空文件夹

> 异步的删除一个空文件夹
>
> 通过添加配置参数 { recursive: true } ，也可以做到删除有内容的文件夹，但nodejs不再推荐该方法
>
> 应当使用 fs.rm() 方法

语法：`fs.rmdir(path[, options], callback)`

- path：*\<string> | \<buffer> | \<url>* 需要删除的空文件夹
- opations：以弃用
- callback：*\<function>* 失败将传入一个 error 参数

```js
fs.rmdir('./item2', (err) => {
    if (err) {
        console.log('错误');
    } else {
        console.log('成功');
    }
})
```





### 删除一个文件

> 异步的删除一个文件
>
> 删除带有内容的文件夹时加上配置参数 { recursive: true }，删除空文件夹时应使用 fs.rmdir()

语法：`fs.rm(path[, options], callback)`

- path：*\<string> | \<buffer> | \<url>* 需要删除的文件
- opations：*\<object>* 配置参数对象
  - force：*\<boolean>* 如果删除失败时忽略异常，默认值 false ，添加该项可以实现类似 `rm -rf` Unix 命令的行为
  - maxRetries：*\<integer>* 如果操作过程中失败将重试，该项为重试次数，默认值 0
  - recursive：*\<boolean>* 执行递归删除（删除里面的文件），操作失败时会重试，该项为是否递归，默认值  false
  - retryDelay：*\<integer>* 重试之间的间隔时间，单位毫秒，默认值 100
- callback：*\<function>* 失败将传入一个 error 参数

> fs.rm() 不仅仅可以删除文件，通过添加配置参数 { recursive: true } 可以实现删除一个带有内容的文件夹（目录）

```js
fs.rm('./item2/text1.txt', (err) => {
    if (err) {
        console.log('错误');
    } else {
        console.log('成功');
    }
})
```





### 读取文件夹/文件的状态

> 异步的读取一个文件夹/文件的状态

语法：`fs.stat(path[,opations], callback)`

- path：*\<string> | \<buffer> | \<url>* 读取的文件
- opations：*\<object>* 配置参数对象
  - bigint：指定返回值是否应该为 bigint 大整数，默认值 false
- callback：*\<function>* 
  - error：失败将传入一个 error 参数
  - stat：返回值，返回的是这个文件夹/文件的参数对象

```js
fs.stat('./item2/file.txt', (err, stat) => {
    if (err) {
        console.log('错误');
    } else {
        console.log('成功');
        console.log(stat);
    }
})
```





### 读取文件目录

> 异步的读取一个文件夹的目录

语法：`fs.readdir(path[,opations], callback)`

- path：*\<string> | \<buffer> | \<url>* 读取的文件
- opations：*\<object>* 配置参数对象
  - encoding：\<string> 默认 = `'utf8'`
  - callback：*\<function>* 
  - error：失败将传入一个 error 参数
  - stat：`<string []> | <Buffer []>` 返回值，返回的是这个文件夹/文件的参数对象

读取一个目录的内容。 回调有两个参数 `(err, files)`，其中 `files` 是目录中不包括 `'.'` 和 `'..'` 的文件名的数组。

可选的 `options` 参数用于传入回调的文件名，它可以是一个字符串并指定一个字符编码，或是一个对象且由一个 `encoding` 属性指定使用的字符编码。 如果 `encoding` 设为 `'buffer'`，则返回的文件名会被作为 `Buffer` 对象传入。 注意: 'path' 的路径是以当前文件为基准进行查找的,而不是运行的时候的相对路径

```js
fs.readdir(__dirname + '/files', (err, result) => {
    if (err) {
        console.log('读取错误');
        return
    }

    console.log(result);
})
```





### 检查一个文件夹/文件是否存在

> 异步的检查一个文件夹/文件是否存在

语法：`fs.access(path[, mode], callback)`

- path：*\<string> | \<buffer> | \<url>* 读取的文件
- mode：*\<integer>* 默认值 `fs.constants.F_OK`
- callback：*\<function>* 
  - error：失败将传入一个 error 参数

> 测试 `path` 指定的文件或目录的用户权限。 `mode` 是一个可选的整数，指定要执行的可访问性检查。 以下常量定义了 `mode` 的可能值。 可以创建由两个或更多个值的位或组成的掩码（例如 `fs.constants.W_OK | fs.constants.R_OK`）。

- `fs.constants.F_OK` - `path` 文件对调用进程可见。 这在确定文件是否存在时很有用，但不涉及 `rwx` 权限。 如果没指定 `mode`，则默认为该值。
- `fs.constants.R_OK` - `path` 文件可被调用进程读取。
- `fs.constants.W_OK` - `path` 文件可被调用进程写入。
- `fs.constants.X_OK` - `path` 文件可被调用进程执行。 对 Windows 系统没作用（相当于 `fs.constants.F_OK`）。

```js
fs.access('./item1', (err) => {
    if (err) {
        console.log('不存在');
    } else {
        console.log('存在');
    }
})
```





### 简单文件写入

> 异步简单文件写入

语法：`fs.writeFile(file, data[, options], callback)`

- file： *\<string> | \<buffer> | \<url> | \<integer>* 要希尔文件的路径+文件名+后缀（不存在的创建）

- data： *\<string> | \<buffer> | \<Uint8Array>* 要写入的数据

- options：*\<string> | \<Object>* 可选配置参数对象

  - encoding：*\<string> | \<null>* 编码格式，默认值  null = `'utf8'`

  - mode：设置文件的操作权限，默认为 0o666（8进制）0o666 = 0o222 + 0o444 即可读可写，

    书写时直接写8进制，勿写字符串。

    - 0o111 文件可被执行的权限 .exe 等
    - 0o222 文件可被写入的权限
    - 0o444 文件可被读取的权限

  - flag：*\<string>* 打开文件执行操作，默认值 `‘w'`

    - a 追加（使用该参数，写入时将变成追加）
    - w 覆盖写入 默认值

- callback：*\<function>* 回调函数

  - error：*\<error>* 错误时将传入错误对象



> 如果 `data` 是一个 buffer，则忽略 `encoding` 选项。它默认为 `'utf8'`。
>
> 如果 `options` 是一个字符串，则它指定了字符编码。

```js
const fs = require('fs');

fs.writeFile('./demo.txt','你好，nodejs',(err)=> {
    if(err) {
        console.log('写入失败');
    } else {
         console.log('写入成功');
    }
});
```





### 流式文件写入

> 流式文件写入

语法： `fs.createWriteStream(path[, options])`

- `path`： *\<string> | \<buffer> | \<url>* 要写入文件的路径+文件名+文件后缀

- options：*\<string> | \<Object>* 可选配置参数对象

  - `flags`：*\<string>* 打开文件执行操作 默认值 w

    - a 追加（使用该参数，写入时将变成追加）
    - w 覆盖写入

  - `encoding`：*\<string>* 设置文件的编码方式，默认为 utf-8

  - `fd`：*\<integer>* 文件统一标识，linux下的文件标识符 默认 null

  - `mode` ：*\<integer>* 设置文件的操作权限，默认为 0o666（8进制）

    0o666 = 0o222 + 0o444 即可读可写，书写时直接写8进制，勿写字符串

    - 0o111 文件可被执行的权限 .exe 等
    - 0o222 文件可被写入的权限
    - 0o444 文件可被读取的权限

  - `autoClose`：*\<boolean>* 流关闭时文件是否自动关闭文件，默认 true

  - `start`：*\<integer>* 写入文件的起始值，例如可从中间开始写（偏移量）填数字



`options` 也可以包括一个 `start` 选项，使其可以写入数据到文件某个位置。 如果是修改一个文件而不是覆盖它，则需要`flags` 模式为 `r+` 而不是默认的 `w` 模式。 `encoding` 可以是任何可以被 `Buffer` 接受的值。



> `options` 是一个带有以下默认值的对象或字符串：
>
> 如果 `options` 是一个字符串，则它指定了字符编码。

```js
const defaults = {
  flags: 'w',
  encoding: 'utf8',
  fd: null,
  mode: 0o666,
  autoClose: true
};
```



```js
// 创建一个可写流
let ws = fs.createWriteStream('./demo.txt');

// 监听可写流
ws.on('open', ()=> {
    console.log('流打开了');
});

// 监听可写流
ws.on('close', ()=> {
    console.log('流关闭了');
});

// 写入数据
ws.write('nodejs，你好啊！');

// 关闭流
ws.close(); // node8 及以下使用该方法关流会造成数据丢失

// ws.end(); // node8 及以下使用该方法
```





### 简单读取文件

> 异步的读取文件

语法：`fs.readFile(path[, options], callback)`

- path： *\<string> | \<buffer> | \<url> | \<integer>* 要读取文件的路径+文件名+后缀
- options：*\<string> | \<Object>* 可选配置参数对象
  - encoding：*\<string> | \<null>* 编码格式，默认值  null
  - flag：*\<string>* 打开文件执行操作，默认值 `‘r'`

- callback：*\<function>* 回调函数
  - error：*\<error>* 错误时将传入错误对象
  - data：*\<string> | \<Buffer>* 读取的数据



> 如果未指定字符编码，则返回原始的 buffer。
>
> 如果 `options` 是一个字符串，则它指定了字符编码。

```js
fs.readFile('./item1/file.txt', (err, data) => {
    if (err) {
        console.log('error');
    } else {
        console.log('成功');
        console.log(data);
    }
})
```





### 流式读取文件

> 流式读取文件

语法：`fs.createReadStream(path[, options])`

- `path`： *\<string> | \<buffer> | \<url>* 要写入文件的路径+文件名+文件后缀

- options：*\<string> | \<Object>* 可选配置参数对象

  - `flags`：*\<string>* 打开文件执行操作 默认值 r

  - `encoding`：*\<string>* 设置文件的编码方式，默认值 null

  - `fd`：*\<integer>* 文件统一标识，linux下的文件标识符 默认值 null

  - `mode` ：*\<integer>* 设置文件的操作权限，默认值 0o666（8进制）

    0o666 = 0o222 + 0o444 即可读可写，书写时直接写8进制，勿写字符串

    - 0o111 文件可被执行的权限 .exe 等
    - 0o222 文件可被写入的权限
    - 0o444 文件可被读取的权限

  - `autoClose`：*\<boolean>* 流关闭时文件关闭，是否自动关闭文件，默认值 true

  - `start`：*\<integer>* 开始位置（偏移量）

  - `end`：*\<integer>* 结束位置（偏移量）

  - `highWaterMark`：*\<integer>* 64 * 1024 => 16kb

> options 是一个带有以下默认值的对象或字符串：
>
> 如果 `options` 是一个字符串，则它指定了字符编码。

```js
const defaults = {
  flags: 'r',
  encoding: null,
  fd: null,
  mode: 0o666,
  autoClose: true,
  highWaterMark: 64 * 1024
};
```

`options` 可以包括 `start` 和 `end` 值，使其可以从文件读取一定范围的字节而不是整个文件。 `start` 和 `end` 都是包括在内的，并且起始值是 0。

例子，从一个 100 字节长的文件中读取最后 10 个字节：

```js
fs.createReadStream('sample.txt', { start: 90, end: 99 });
```



不同于在一个可读流上设置的 `highWaterMark` 默认值（16 kb），该方法在相同参数下返回的流具有 64 kb 的默认值。

```js
// 创建一个可读流
let rs = fs.createReadStream('./item1/img.jpeg');

// 监听可读流
rs.on('open', () => {
    console.log('可读流以打开');
})

// 监听可读流
rs.on('close', () => {
    console.log('可读流以关闭');
})

// 可读流绑定一个 data 事件，则触发可读流自动读取，可读流读取完成会自动关闭流
rs.on('data', (data) => {
    console.log(data);
})
```





### 待补充

