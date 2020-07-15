#Vuex

Vuex 是一个专为 Vue.js 应用程序开发的**状态管理模式**。它采用集中式存储管理应用的所有组件的状态，并以相应的规则保证状态以一种可预测的方式发生变化。简单的说就是为了解决组件间的数据传递 .

##安装Vuex

1. 直接下载 / CDN 引用 : https://unpkg.com/vuex
2. 在 Vue 之后引入 vuex 会进行自动安装：
```html
<script src="/path/to/vue.js"></script>
<script src="/path/to/vuex.js"></script>
```
使用NPM :
```sh
npm install vuex --save
```
在一个模块化的打包系统中，您必须显式地通过 Vue.use() 来安装 Vuex：
```js
import Vue from 'vue'
import Vuex from 'vuex'

Vue.use(Vuex)
```

>注意 : Vuex 依赖 Promise。
当使用全局 script 标签引用 Vuex 时，不需要以上安装过程。

##官方文档

每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state)。Vuex 和单纯的全局对象有以下两点不同：
1. Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。
2. 你不能直接改变 store 中的状态。**改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。**这样使得我们可以方便地跟踪每一个状态的变化，从而让我们能够实现一些工具帮助我们更好地了解我们的应用。
>其他位置也可以更改store中的数据 , 但这都属于非法的 , 不便于管理和维护 . 

##核心概念

###State

`stata` 对象用来存储组件间要共享的数据，并且是  Vuex  数据共享中的 **唯一数据源** 。 `stata`是 Vuex 核心中的核心。 要访问 state 中数据可以使用**`this.$store.state['attrName']`**,由于 store 对象在实例化` vue` 对象已注入，所以在组件中直接通过 this.$store.state 就可以访问。

###Mutation

mutation中包含了一个回调函数，在这个函数中可以合法的修改 state 成员的值。这个回调函数不能直接调用，类似事件需要通过 store.commit() 函数触发。

### Action

action中可以同时操作多个 mutation 。当然action也可以传入参数，在action中可以包含任意异步操作.

### Getter

getter类似于计算属性。getter也会被缓存，只有当数据发生变化才会重新执行.

###Module

store 模块化管理，每个模块都可以拥有state、mutation、action、getter。在项目中如果有多个组件时可以为每个组件都写一个store模块这样可以便于代码的维护管理。

