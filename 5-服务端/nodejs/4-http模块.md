## http模块

`http` 是一个内置模块



**导入:**

```js
const fs = require('fs')
```





## 创建一个服务

使用 `http` 模块中的 `createServer` 函数创建一个服务



**语法:**

```js
http.createServer([options][, requestListener])
```



**参数:**

- `options` *<Object>*  配置对象
- `requestListener`  *<Function>* 回调函数





## 监听一个端口

当使用 `http.createServer` 创建服务后 , 可以使用其身上的 `listen()` 方法对端口进行监听



**语法:**

```js
server.listen(handle[, backlog][, callback])
server.listen(options[, callback])
server.listen(path[, backlog][, callback]) 用于IPC服务器
server.listen([port[, host[, backlog]]][, callback]) 对于 TCP 服务器
```





## 搭建web服务器

```js
const http = require('http');

// 创建 web 服务
let server = http.createServer((request, response) => {
    response.end('hello nodejs');
});

// 启动服务，监听端口
server.listen('3000', (err) => {
    if (err) {
        console.log('服务器启动失败');
    } else {
        console.log('服务器启动成功');
    }
})
```



## request  请求

> 对请求数据的封装



### 获取请求行信息



#### 获取请求类型

> request.method

```js
request.method

// GET / POST
```



#### 获取请求路径

> request.url

```js
request.url

// /user/?age=19&sex=man
```



> 旧版解析url，存在一定安全隐患（结构化，不用手动对字符串进行分割）
>
> 使用 url.parse()

语法：`url.parse(urlString[, parseQueryString[, slashesDenoteHost]])`

- urlString：\<string> 要解析的 URL 字符串。
- parseQueryString：\<boolean> 如果为 `true`，则 `query` 属性总会通过 `querystring` 模块的 `parse()` 方法生成一个对象。 如果为 `false`，则返回的 URL 对象上的 `query` 属性会是一个未解析、未解码的字符串。 默认为 `false`。
- slashesDenoteHost：\<boolean> 如果为 `true`，则 `//` 之后至下一个 `/` 之前的字符串会被解析作为 `host`。 例如，`//foo/bar` 会被解析为 `{host: 'foo', pathname: '/bar'}` 而不是 `{pathname: '//foo/bar'}`。 默认为 `false`。

`url.parse()` 方法会解析一个 URL 字符串并返回一个 URL 对象。

如果`urlString`不是字符串将会抛出`TypeError`。

如果`auth`属性存在但无法编码则抛出`URIError`。

```js
const url = require('url');

let server = http.createServer((request, response) => {
    let myUrl = url.parse(request.url,  true); // 添加 true 将会把查询字符串解析为对象
    console.log(myUrl);
    response.end('hello nodejs');
})

server.listen(5000, (err) => {
    if (err) {
        console.log('服务启动失败');
        return;
    }
    console.log('服务器启动成功');
})
```





#### 获取协议版本号

> request.httpVersion

```js
request.httpVersion

// 1.1
```



### 获取请求头信息

> request.headers
>
> 返回一个对象，包含请求头的所有信息

```js
request.headers

// 请求头示例
{
  host: 'localhost:5000',      
  connection: 'keep-alive',    
  'cache-control': 'max-age=0',
  'sec-ch-ua': '"Google Chrome";v="107", "Chromium";v="107", "Not=A?Brand";v="24"',
  'sec-ch-ua-mobile': '?0',
  'sec-ch-ua-platform': '"Windows"',
  'upgrade-insecure-requests': '1',
  'user-agent': 'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/107.0.0.0 Safari/537.36',
  accept: 'text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9',
  'sec-fetch-site': 'cross-site',
  'sec-fetch-mode': 'navigate',
  'sec-fetch-user': '?1',
  'sec-fetch-dest': 'document',
  'accept-encoding': 'gzip, deflate, br',
  'accept-language': 'zh-CN,zh;q=0.9,en;q=0.8,ja;q=0.7'
}
```



### 获取请求体信息

> 绑定 data 事件获取请求体
>
> 监听 end 事件，当该请求结束时进行响应
>
> querystring <a href="https://nodejs.org/dist/latest-v18.x/docs/api/querystring.html" target="_blank"> nodejs文档</a>>



```html
<h1>HTTP</h1>
<div>
    <form action="http://localhost:5000" method="post">
        <p>
            <span>姓名：</span><input type="text" name="name">
        </p>
        <p>
            <span>密码：</span><input type="password" name="password">
        </p>
        <button type="submit">提交</button>
    </form>
</div>
```



```js
// 引入解析模块
const qs = require('querystring');

// get 请求体为空，所以进行滤掉
if (request.method.toLocaleUpperCase() === 'POST') {
    // 获取post请求体内容
    let postData = '';
    
    // 从这个数据流中读取数据
    request.on('data', (data) => {
        postData += data;
    });

    request.on('end', () => {
        let parse = qs.parse(postData); // 解析查询字符串封装成一个对象
        console.log(parse);
        response.end('over');
    });
} else {
    response.end('is no post');
}

// [Object: null prototype] { name: '你好', password: '123456' }
```



## response 响应

> 对请求进行响应



### 设置响应状态码

> response.statusCode

```js
response.statusCode = 404;
```



### 设置响应头

>  response.setHeader()

```js
// 自定义响应头
response.setHeader('name', 'rgbcode');

// 设置响应数据类型为 html
response.setHeader('content-type', 'text/html');

// 设置响应数据类型为 html , 并且字符编码为 utf-8
response.setHeader('content-type', 'text/html;charset=utf-8');

// 设置响应数据类型为 纯文本(字符串)
response.setHeader('content-type', 'text/plain');
```



>  response.writeHead()

语法：`response.writeHead(statusCode[, statusMessage][, headers])`

- statusCode：number ，状态码
- statusMessage：string ，可选的状态描述
- headers：object ，响应头

```js
response.writeHead(200, {
    'content-type': 'text/html;charset=utf-8'
})
```



### 设置响应体

> response.write()
>
> 或者直接在 response.end() 中设置

```js
response.write('<h1>over</h1>');
response.end();

// 或者
response.end('<h1>over</h1>');
```



