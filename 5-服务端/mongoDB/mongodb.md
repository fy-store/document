# mongoDB

> 属于非关系型数据库

关系型和非关系型两者特点，待补充。

主要应用场景，待补充。



- mongodb数据库系统 => 具体数据库(如用户信息) => 集合(如登录信息) => 文档(小明的信息) => 字段(name: xiaoming)



## 配置环境

下载地址：<a href="https://www.mongodb.com/try/download/community2" target="_blank">官网下载</a>

注意点：

使用安装包安装。

安装后需要在C盘根目录下创建一个data文件夹，并在其内继续创建一个db文件夹，用于存放保存的数据。

还需在 data 下继续创建一个 log 文件夹，用于存放日志。

原因是因为默认目录保存位置。

<hr>

在 mongodb的安装目录下 bin 的同级创建一个文件 mongod.cfg ，作为配置文件使用。

这是作为window的一个批量启动文件使用，让我们一开启电脑自动启动数据库服务。

文件内容为：

```sh
systemLog:
	destination: file
	path: c:\data\log\mongod.log
storage:
	dbPath: c:\data\db
net:
	port: 27017
```



而后以管理员身份执行以下命令：

```sh
sc.exe create MongoDB binPath= "\"D:\web\mongoDB\bin\mongod.exe\" --service --config="D:\web\mongoDB\mongod.cfg\"" DisplayName="MongoDB" start="auto"
```



已存在则 sc delete MongoDB



若无用则在资源管理器用户手动配置



## 常用命令

**启动数据库服务**

```sh
mongod
```



**连接数据库**

```sh
mongo
```



**修改端口**

mongodb 默认端口号为 27017

建议4位以上，最大不超过 6553

```sh
--port

示例：
--port 27018
```



**修改默认目录** 

mongodb 默认保存数据的目录是C盘下的 data/db

```sh
--dbpath
```

 

**查看当前在操作的数据库**

```sh
db
```



**查看数据库列表（如果数据库为空，则不出现在列表中）**

```sh
show dbs
```



**切换数据库（如果不存在则创建一个)**

```sh
use xxx
```



**向当前数据库的xxx集合中插入一个文档**

```sh
db.xxx.insert()
```



**展示当前数据库中所有的集合**

```sh
show collections
```



## 删除数据库

```sh
db.dropDatabase()
```





## 增删改查

> 常用增删改查



**逻辑操作符**

```sh
// 在使用操作符时需要使用转义字符代替

<    $lt  

<=   $lte 

>    $gt 

>=   $gte 

!==  $ne 
```



**逻辑运算符与或非**

```sh
逻辑或：使用$in 或 $or
查找年龄为18或20的学生
举例：db.students.find({age:{$in:[18,20]}})
举例：db.students.find({$or:[{age:18},{age:20}]})

3.逻辑非：$nin

4.正则匹配：
举例：db.students.find({name:/^T/})

5.$where能写函数：
db.students.find({$where:function(){
    return this.name === 'zhangsan' && this.age === 18
}})
```



**增：**

```sh
// 插入一条文档
db.集合名.insert(文档对象);
db.集合名.insertOne(文档对象);

// 插入多条文档
db.集合名.insertMany([文档对象, 文档对象, ...]);
```



**查：**

```sh
db.集合名.find(查询条件[,投影]);

// 查询所有
db.xxx.find({});

// 查询所有age === 18 的数据
db.xxx.find({age:18});

// 查询所有age === 18 并且 sex === '男' 的数据
db.xxx.find({age:18, sex:'男'});

// 查询所有age === 18 的数据
// 设置投影，不要_id 不要sex （只能出现1或者0，不可以同时出现，但是_id可以，是例外）
db.xxx.find({age:18},{_id:0, sex:0});
    
// 查询age于20的
// 给它一个描述对象
db.xxx.find({age:{$gte:20}});
```

**投影：**

过滤掉不想要的数据，只保留想要展示的数据
举例：db.students.find({},{_id:0,name:0}),过滤掉id和name
举例：db.students.find({},{age:1}),只保留age
补充：db.集合名.findOne(查询条件[,投影])，默认只要找到一个



**改：**

```shell
db.集合名.update(查询条件,要更新的内容[,配置对象])

//如下写法会将更新内容替换掉整个文档对象，但_id不受影响
举例：db.students.update({name:'zhangsan'},{age:19})

//使用$set修改指定内容，其他数据不变，不过只能匹配一个zhangsan
举例：db.students.update({name:'zhangsan'},{$set:{age:19}})

//修改多个文档对象，匹配多个zhangsan,把所有zhangsan的年龄都替换为19
举例：db.students.update({name:'zhangsan'},{$set:{age:19}},{multi:true})

补充：db.集合名.updateOne(查询条件,要更新的内容[,配置对象])
db.集合名.updateMany(查询条件,要更新的内容[,配置对象])
```

**删：**

```shell
db.集合名.remove(查询条件)
//删除所有年龄小于等于19的学生
举例：db.students.remove({age:{$lte:19}})
```





## 配置密码

**启动 mongod 带验证码选项**

```shell
mongod --auth
```



**创建一个用户**

```sh
mongo

use admin

db.createUser({user:"setAdmin",pwd:"password",roles:["root"]});
```



**命令行连接数据库**

```sh
mongo

use admin

db.auth("user","password");
```



**mongoose连接**

```js
mongoose.connecte('mongodb://user:password@localhost:27017/prepare?authSource=admin');
```

