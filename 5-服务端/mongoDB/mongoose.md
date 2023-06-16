# mongoose

> mongoose：在Node平台下，一个知名的用于帮助开发者连接mongoDB的包

为什么用mongoose？ 

想在Node平台下，更加简单、高效、安全、稳定的操作mongoDB

```npm
npm i mongoose / yarn add mongoose
```



```js
// 导入 mongoose
const mongoose = require('mongoose');

// 连接数据库 person_info，如果不存在则创建
mongoose.connect('mongodb://localhost:27017/person_info');

mongoose.connection.on('open', () => {
    console.log('数据库连接成功');

    // 创建文档结构
    let info = new mongoose.Schema({
        name: String,
        age: Number,
        sex: String
    });

    // 创建文档模型，集合命名 person_infos
    let infoModel = mongoose.model('person_infos', info);

    // 使用文档模型添加数据(添加一条文档)
    infoModel.create({
        name: '呵呵', // name 字段
        age: 19,	 // age 字段
        sex: '男'	// sex 字段
    }, (err, data) => {
        if (err) {
            console.log('添加数据失败');
        } else {
            console.log(data);
            console.log('添加数据成功');
            // mongoose.connection.close(); 关闭数据库连接，一般不用
        }
    })
})
```



## 事件

**数据库连接成功**

```js
mongoose.connection.on('open', () => {})
```



**数据库连接失败**

```js
mongoose.connection.on('error', () => {})
```





## 增加数据

> Model.create()



**增加一条数据(文档)**

语法：`model.create(obj [,option] [,callback])`

- obj `<object>` 需要添加的数据(文档)
- option `<obj>` 可选配置参数
- callback `<function>` 回调函数
  - err 错误参数
  - data 添加的数据

```js
testModel.create({
    name: 'test',
    age: 19
}, (err, data)=>{});
```



**批量增加数据(文档)**

语法：`model.create(arr[obj, obj, ...] [,callback])`

- arr `<array>` 包裹数据的数组
  - obj `<object>` 需要添加的数据(文档)

- callback `<function>` 回调函数
  - err 错误参数
  - data 添加的数据

```js
testModel.create([
    {
    	name: 'test1',
    	age: 19
	},
    {
        name: 'test2',
        age: 18
    }
], (err, data)=>{});
```





## 删除数据

> Model.deleteOne() 和 Model.deleteMany() 



**删除第一条数据(文档)**

语法：`model.deleteOne(conditions [,option] [,callback])`

- conditions `<obj>` 查询条件对象
- option `<obj>` 可选配置参数
- callback `<function>` 回调函数
  - err 错误参数
  - info 删除成功的信息

```js
infoModel.deleteOne({ name: '小明' }, (err, info) => {
    if (err) {
        console.log('删除失败');
    } else {
        console.log(info);
        console.log('删除成功');
    }
})
```



**批量删除数据(文档)**

语法：`model.deleteMany(conditions [,option] [,callback])`

- conditions `<obj>` 查询条件对象
- option `<obj>` 可选配置参数
- callback `<function>` 回调函数
  - err 错误参数
  - info 删除成功的信息

```js
infoModel.deleteMany({ age: 19 }, (err, info) => {
    if (err) {
        console.log('删除失败');
    } else {
        console.log(info);
        console.log('删除成功');
    }
})
```





## 修改数据

> Model.updateOne() 和 Model.updateMany()



**修改第一条数据**

语法：`model.updateOne(filter, update [,option] [,callback])`

- filter `<object>` 需要修改的数据(文档)
- update `<object>` 更新的数据
- option `<object>` 配置对象
- callback `<function>` 回调函数
  - err 错误参数
  - info 删除成功的信息

```js
infoModel.updateOne({ name: '小王' }, { name: '小张' }, (err, info) => {
    if (err) {
        console.log('更新失败');
    } else {
        console.log(info);
        console.log('更新成功');
    }
})
```



**批量修改数据**

语法：`model.updateMany(filter, update [,option] [,callback])`

- filter `<object>` 需要修改的数据(文档)
- update `<object>` 更新的数据
- option `<object>` 配置对象
- callback `<function>` 回调函数
  - err 错误参数
  - info 删除成功的信息

```js
infoModel.updateMany({ age: 18 }, { age: 19 }, (err, info) => {
    if (err) {
        console.log('更新失败');
    } else {
        console.log(info);
        console.log('更新成功');
    }
})
```





## 查询数据

> Model.findOne() 和 Model.find()



**查询第一条数据**

语法：`model.findOne([conditions] [,projection] [,options] [,callback])`

- conditions `<object>` 查询的对象
- projection `<Object|String|Array[String]>` 要返回的字段
- option `<object>` 配置对象
- callback `<function>` 回调函数
  - err 错误参数
  - data 查询成功的数据

```js
infoModel.findOne({ name: '小王' }, (err, data) => {
    if (err) {
        console.log('查询失败');
    } else {
        console.log(data);
        console.log('查询成功');
    }
})
```



**通过 id 查询数据**

语法：`model.findById(_id [,projection] [,options] [,callback])`

- _id `<object>` 查询的对象的 _id
- projection `<Object|String|Array[String]>` 要返回的字段
- option `<object>` 配置对象
- callback `<function>` 回调函数
  - err 错误参数
  - data 查询成功的数据

```js
infoModel.findById('63808a340fe67a4f6834e5bd', (err, data) => {
    if (err) {
        console.log('查询失败');
    } else {
        console.log(data);
        console.log('查询成功');
    }
})
```



**批量查询数据**

语法：`model.find(filter [,projection] [,options] [,callback])`

- filter `<object>` 查询的对象
- projection `<Object|String|Array[String]>` 要返回的字段
- option `<object>` 配置对象
- callback `<function>` 回调函数
  - err 错误参数
  - data 查询成功的数据

```js
infoModel.find({ age: 19 }, (err, data) => {
    if (err) {
        console.log('查询失败');
    } else {
        console.log(data);
        console.log('查询成功');
    }
})
```



**查询该集合下所有数据**

`model.find({})` 或者 `model.find()`
