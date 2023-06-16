## npm 上传一个包

**查看当前源：**

```cmd
npm config get registry
```



**切换为npm源：**

```npm
npm config set registry https://registry.npmjs.org
```



**切换为淘宝镜像：**

```cmd
npm config set registry=https://registry.npm.taobao.org/
```



**查询包是否存在:**

```cmd
npm view 你的npm包名
```



**添加用户:**

```cmd
npm adduser
```



**查看当前账户:**

```cmd
npm who am i
```



**上传包:**

后续更新包时修改 *package.json* 的 *verson* 版本号后再重新上传

```cmd
npm publish
```



**命令行修改版本:**

它会将package.json中的version版本加0.0.1

```cmd
npm version patch
```



**删除指定包版本:**

```cmd
npm unpublish 包名@版本号
```



**删除整个包:**

```cmd
npm unpublish 包名 --force
```

