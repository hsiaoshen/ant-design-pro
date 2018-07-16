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



