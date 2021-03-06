# 关于ant-design-pro的基本描述和概念

项目设计到的技术有：react + es + dva + redux + nodejs + wepack + babel + fetch + mock

## reactJs的意义和工作原理

意义：变化的数据实时的显示在UI上，减少了对DOM的频繁操作，提高了性能。

实现位置：浏览器

工作原理：每次渲染react会构建虚拟DOM树，然后与上一个虚拟DOM树进行了diff比较，得到DOM结构的区别，然后仅仅将需要变化的部分进行实际的浏览器DOM更新。

注意：在事件循环当中，多次数据会被合并。开发者只需要关注在某个数据状态下，如何render整个页面


## dva-cli

用于初始化项目，形成规范的项目目录结构

```
$ npm install dva-cli -g
$ dva init
```

### 生成的目录结构分析

1. mock: mock生成的模拟数据存放位置
2. public: 存放静态文件，打包时直接复制到输出目录为(./dist)
3. src： 存放项目源代码

    1. assets: 用于存放静态资源
    2. components: 用于存放React组件，一般是该项目的无状态组件
    3. models: 用于存发放模型文件
    4. routes: 用于存放需要 connect model 的路由组件
    5. services: 用于存放服务文件，一般是网络请求等
    6. utils: 工具类库
    7. router.js: 路由文件
    8. index.js: 项目的入口文件
 
### model

一个项目对应一个model

基本model如下：

1. namespace: 该模块的命名空间，也是state上的一个属性，只能为字符串且不可创建多层空间
2. state: 初始状态
3. reducer： 是唯一可以修改state的地方，由action触发，state和action2个参数(处理同步操作)
4. effects: 用于处理异步操作，不能直接修改 state，由 action 触发，也可触发 action。有2个参数action和effects(put--触发action, call--调用异步处理逻辑, select--从state中获取数据)


**注意**： 在model里面触发action时不需要携带namespace, 组件中触发需要在action前添加namespace

### app

```js
import dva from 'dva';
var app = dva({
    initialState: {}
})

// 初始化的state优先高于model中的state
```

### connect

组件和model的连接采用connect

```js
import React from 'react';
import { connect } from 'dva';

const User = ({ dispatch, user }) => {
  return (
    <div></div>
  )
}

export default connect(({ user }) => {
  return user;
})(User);

```

## 弄懂以下问题

### react的生命周期

1. Mounting: 插入真实的DOM

    1. commponentWillMount: 渲染前调用，在客户端和服务端
    2. commponentDidMount: 渲染之后调用，在客户端
    
2. Updating：重新渲染

    1. componentWillReceiveProps: 接受新的state或者prop时调用，初始化渲染不调用
    2. shouldComponentUpdate: 返回一个布尔值, 在组件接收到新的props或者state时被调用。在初始化时或者使用forceUpdate时不被调用。 
    3. componentWillUpdate： 在组件接收到新的props或者state但还没有render时被调用。在初始化时不会被调用
    4. componentDidUpdate: 在组件完成更新后立即调用。在初始化时不会被调用。
    
3. Unmounting: 移除真实的DOM

    1. componentWillUnmount: 在组件从 DOM 中移除的时候立刻被调用。


## antd pro start

### 集成化安装

```sh
$ npm install ant-design-pro-cli -g 
$ mkdir my-project && cd my-project 
$ pro new # 安装脚手架 
```

### 实现过程

在浏览器上输入路径 --> 脚本架获取路径（dva） --> common种匹配路径 --> 加载layouts页面 --> router页面 --> 调用dispatch()请求数据，加载 --> 加载model模型，并调用services请求 --> 参数传到components控制 --> 加载components --> 渲染返回html

### 技术详解

#### dva-createLoading

只做一次状态处理，每次请求期间都会触发loading状态

原因:global属性

```js
import createLoading from 'dva-loading';
var app = dva();
app.use(createLoading())
```
#### 

### 开发需要做

1. common种添加新页面的path
2. routers中增加新路由页面
3. 需要复用的components封装
4. models新增模型
5. services增加请求


### 备注

1. antd是样式，antd pro是框架
2. antd pro 有自己的权限控制体系 Authorized
3. dva请求一步，有自己的方法获取到结果或者错误
4. style中的样式用驼峰法 





