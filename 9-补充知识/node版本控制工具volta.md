# volta

volta 是node的版本控制工具 . 

**github:** https://github.com/volta-cli/volta





## 安装最新版本node

```bash
volta install node@latest
```





## 安装指定版本node

安装指定版本，比如14.5.0

```bash
volta install node@14.5.0
```





## 查看安装环境

查看当前环境依赖

```bash
volta list
```



查看所有环境依赖

```bash
volta list all 
```





## 项目node版本控制

- 我们有了多个版本的node，就可以到项目中进行对应的设置了
- 比如我们vue2的项目需要14版本的node，前往项目目录执行命令
- 该命令用于可用于指定全局使用的node版本, 或指定项目node版本 . 

```bash
volta pin node@14
```



- 如果我们使用 `node@14`，volta会帮助我们找14中最合适的版本，可能不是我们安装过的版本，如果想使用我们安装的版本，必须把版本号写全

```bash
volta pin node@14.5.0
```



- 此时我们的项目`package.json`中会多一个配置

```bash
"volta": {
  "node": "14.5.0"
}
```





## 常用命令

```bash
volta list //查看当前环境的版本
volta list all //查看存在的所有版本
volta install node //安装最新版的nodejs
volta install node@12.2.0 //安装指定版本
volta install node@12 //volta将选择合适的版本安装
volta pin node@10.15 //将更新项目的package.json文件以使用工具的选定版本
volta pin yarn@1.14 //将更新项目的package.json文件以使用工具的选定版本
```





## 注意事项

window 出现权限问题: 

一般出现全局安装失败, 无法安装等 . 

在本地搜索里搜 [命令提示符] => 以管理员打开, 在此终端中进行操作
