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



