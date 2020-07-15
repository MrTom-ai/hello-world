# Vue的简介,插值和指令

## [Vue.js 是什么](https://cn.vuejs.org/v2/guide/#Vue-js-%E6%98%AF%E4%BB%80%E4%B9%88)

Vue (读音 /vjuː/，类似于 **view**) 是一套用于构建用户界面的**渐进式框架**。与其它大型框架不同的是，Vue 被设计为可以自底向上逐层应用。**Vue 的核心库只关注视图层**，不仅易于上手，还便于与第三方库或既有项目整合。另一方面，当与[现代化的工具链](https://cn.vuejs.org/v2/guide/single-file-components.html)以及各种[支持类库](https://github.com/vuejs/awesome-vue#libraries--plugins)结合使用时，Vue 也完全能够为复杂的单页应用提供驱动。 Vue是单页面应用程序。

[下载地址](https://cn.vuejs.org/v2/guide/installation.html )

可以在官网下载，也可以命令行输入
先输入npm init --yes 在输入 npm i vue -g

> ### 注意:安装路径不能有中文 ! ! !

注意 : 以下 `vm`为实例化的Vue对象

### [el](https://cn.vuejs.org/v2/api/#el)

- **类型**：`string | Element`

- **限制**：只在用 `new` 创建实例时生效。

- **详细**：

  提供一个在页面上已存在的 DOM 元素作为 Vue 实例的挂载目标。可以是 CSS 选择器，也可以是一个 HTMLElement 实例。

  在实例挂载之后，元素可以用 **`vm.$el` **访问。

  如果在实例化时存在这个选项，实例将立即进入编译过程，否则，需要显式调用 **`vm.$mount()`** 手动开启编译。

> 提供的元素只能作为挂载点。不同于 Vue 1.x，所有的挂载元素会被 Vue 生成的 DOM 替换。因此不推荐挂载 root 实例到 `<html>` 或者 `<body>` 上。 

> 如果 `render` 函数和 `template` property 都不存在，挂载 DOM 元素的 HTML 会被提取出来用作模板，此时，必须使用 Runtime + Compiler 构建的 Vue 库。 

### [data](https://cn.vuejs.org/v2/api/#data)

- **类型**：`Object | Function`

- **限制**：组件的定义只接受 `function`。

- **详细**：

  Vue 实例的数据对象。Vue 将会递归将 data 的 property 转换为 getter/setter，从而让 data 的 property 能够响应数据变化。**对象必须是纯粹的对象 (含有零个或多个的 key/value 对)**：浏览器 API 创建的原生对象，原型上的 property 会被忽略。大概来说，data 应该只能是数据 - 不推荐观察拥有状态行为的对象。

  一旦观察过，你就无法在根数据对象上添加响应式 property。因此推荐在创建实例之前，就声·明所有的根级响应式 property。

  实例创建之后，可以通过 `vm.$data` 访问原始数据对象。Vue 实例也代理了 data 对象上所有的 property，因此访问 `vm.a` 等价于访问 `vm.$data.a`。

  以 `_` 或 `$` 开头的 property **不会**被 Vue 实例代理，因为它们可能和 Vue 内置的 property、API 方法冲突。你可以使用例如 `vm.$data._property` 的方式访问这些 property。

  当一个**组件**被定义，`data` 必须声明为返回一个初始数据对象的函数，因为组件可能被用来创建多个实例。如果 `data` 仍然是一个纯粹的对象，则所有的实例将**共享引用**同一个数据对象！通过提供 `data` 函数，每次创建一个新实例后，我们能够调用 `data` 函数，从而返回初始数据的一个全新副本数据对象。

  如果需要，可以通过将 `vm.$data` 传入 `JSON.parse(JSON.stringify(...))` 得到深拷贝的原始数据对象。

> 注意，如果你为 `data` property 使用了箭头函数，则 `this` 不会指向这个组件的实例，不过你仍然可以将其实例作为函数的第一个参数来访问。 

## 插值 

`{{value}}` value需要定义在`data`中 `value`可以是任意类型 , **绑定数据类型(1)**

```html
<body>
    <div id="app">
        {{m}}
        <h2>{{obj.name}}</h2>
        <h2>{{obj.age}}</h2>
        <h3>{{num}}</h3>
        <h4>{{arr}}</h4>
        <h4>{{arr[3]}}</h4>
    </div>

    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        new Vue({
            el:'#app',
            data:{
                m:1,
                obj:{name:"晓",age:18},
                num:123,
                arr:[12,3,45,66,33,1]
            }
        })
    </script>
</body>
```

## 指令

- ### [v-bind](https://cn.vuejs.org/v2/api/#v-bind)

  - 给标签元素的属性绑定值 ,**绑定数据类型(2)**
  - `:` 缩写
  - 绑定`class` 和`style`属性时值支持json格式和数组

```html
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .box1{
            height: 100px;
            background: red;
            display: none;
        }
        .show{
            display: block;
        }
    </style>
</head>
<body>
    <div id="root">
        <ul :class='[a1,a2]'></ul>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        Vue.config.devtools = true
        new Vue({
            el:'#root',
            data:{
                a1:'box1',
                a2:{show:false},
            },
        })
    </script>
</body>
```



- ### [v-html](https://cn.vuejs.org/v2/api/#v-html)

  - 更新元素的 `innerHTML`。**绑定数据类型(2)**，谨慎使用该指令，容易造成DOM文档的内容被篡改。
  - **注意：内容按普通 HTML 插入 - 不会作为 Vue 模板进行编译**。如果试图使用 `v-html` 组合模板，可以重新考虑是否通过使用组件来替代。如果有标签就按HTML语法将标签转为节点渲染到页面 。


```html
<h2 v-html='h2h'></h2>
```

```vue
data：{h2h: '<a href="https://www.baidu.com" target="_block">baidu</a>'}
```

- ### [v-text](https://cn.vuejs.org/v2/api/#v-text) 

  -  原理与innerText一致。绑定数据类型(2)，内容是纯文本直接渲染到页面。

- ### [v-for](https://cn.vuejs.org/v2/api/#v-for)

  -  **列表渲染,常用来动态创建组件** 。

```html
<body>
    <ul id="app">
        <li v-for="(val,key,index) in obj">信息 {{index+1}} : {{key}} : {{val}}</li>
    </ul>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        Vue.config.devtools = true
        new Vue({
            el: '#app',
            data: {
                obj:{
                    name:'法外狂徒张三',
                    age:'18',
                    job:'学生'
                }
            }
        })
    </script>
</body>
```



- ### [v-if](https://cn.vuejs.org/v2/api/#v-if),[v-else-if](https://cn.vuejs.org/v2/api/#v-else-if), [v-else ](https://cn.vuejs.org/v2/api/#v-else) 

  - 用于条件渲染
  - 语意上与原生js中的`if`条件没有什么本质上的区别 ，` v-else-if`和js中的`else if`语句一样可以有多个,`v-else`在末尾,有且只有一个。在vue的虚拟DOM中`v-if,v-else-if,v-else`相互切换，在真正的DOM中，当其中一个执行时，另外两种指令会将其里面整个内容全部”干掉“，变成`<!---->`。

```html
<body>
    <div id="root">
        <ul :class='list'>
            <li v-if="1 === num">red</li>
            <li v-else-if="2 === num">blue</li>
            <li v-else-if="3 === num">green</li>
            <li v-else-if="4 === num">pink</li>
            <li v-else></li>
        </ul>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        new Vue({
            el:"#root",
            data:{

            },
        })
    </script>
</body>
```

- ### [v-show](https://cn.vuejs.org/v2/api/#v-show)

  - 条件渲染 : 效果与`v-if`类似 , 但当条件为false时不会将元素从DOM中去掉 ，只会改变display属性为 ’none‘ 。

```html
<body>
    <div id="root">
        <h1 v-show="show">你好</h1>
    </div>
    <script src="./vue.min.js"></script>
    <script>
        Vue.config.devtools = true
        new Vue({
            el: "#root",
            data: {
                show: true,
            },
        })
    </script>
</body>
```

> `v-if`显示或隐藏时会动态的添加或删除DOM元素，而`v-show`显示或隐藏只是修改css属性display:none实现的。 如果频繁那么请使用`v-show`，反之使用`v-if`

- ### [v-model](https://cn.vuejs.org/v2/api/?#v-model)

  - **预期**：随表单控件类型不同而不同。

  - **限制**：

    - `<input>`
    - `<select>`
    - `<textarea>`
    - components

  - **修饰符**：

    - [`.lazy`](https://cn.vuejs.org/v2/guide/forms.html#lazy) - 事件状态的改变，将`input`事件变成`onchange`事件
    - [`.number`](https://cn.vuejs.org/v2/guide/forms.html#number) - 输入字符串转为有效的数字，一般用于数字类型的输入框，将字符串类型的数字转换为数字类型。
    - [`.trim`](https://cn.vuejs.org/v2/guide/forms.html#trim) - 去掉输入文本首尾的空格。

  - **用法**：

    可以在表单控件或者组件上创建双向绑定。用法如下:

    ```html
        <body>
            <div id="app">
                <input type="text" v-model="inputText">
    			//进行双向绑定
                <h2>{{ inputText }} </h2>
            </div>
            <script src="./lib/vue.js"></script>
            <script>
                new Vue({
                    el: '#app',
                    data: {
                        inputText: 'hello model'
                    }
                })
            </script>
        </body>
    ```

  - 在表单控件中`[text='checkbox']`中,如果只有一个,`v-model`的值为boolean.如果有多个,则`v-model`的值为控件的value

  在body中:

  ```html
  <div id='app'>
      <input type="checkbox" id="cc" v-model='cc'>
      <br>
      <input type="checkbox" name="color" value="red" id="red" v-model='selectColor'>
      <label for="red">red</label>
      <input type="checkbox" name="color" value="blue" id="blue" v-model='selectColor'>
      <label for="blue">blue</label>
      <input type="checkbox" name="color" value="green" id="green" v-model='selectColor'>
      <label for="green">green</label>
      <h2>{{selectColor}}</h2>
  </div>
  ```

  在script中:

  ```js
  new Vue({
           el: '#app',
           data: {
                 cc: false,
                 selectColor:[],
                  }
              })
  ```

  - 在表单控件`<select>`中 , `v-model`的值为`<option>`的value

  在body中

  ```html
  <div id='app'>
  	<select name="city" v-model='seclectValue'>
         <option disabled value="">请选择</option>
         <option value="zh">深圳</option>
         <option value="gz">广州</option>
         <option value="dg">东莞</option>
         <option value="fs">佛山</option>
  	</select>
  	<h2>{{seclectValue}}</h2>
  </div>
  ```

  在script中

  ```js
  <script>
              new Vue({
                  el: '#app',
                  data: {
                      seclectValue: '',
                  }
              })
  </script>
  ```

  - 修饰符的使用

    - `.number`的使用:
      - 语法:`v-model.number="xxx"`
      - 输入框的必须是数字才会有效,一般配合表单控件`[type='number']`使用
    - `.lazy`的使用:
      - 语法:`v-model.lazy="xxx"`
      - 当进行数据双向绑定时,`.lazy`功能类似将事件类型从`oninput`转`onchange`

    ```html
    <body>
            <div id="app">
                <input type="number" v-model.number.lazy='getNum'>
                <h2>{{getNum+1}}</h2>
                <input type="text" v-model.trim='str'>
                <pre>{{str}}</pre>
            </div>
            <script src="./lib/vue.js"></script>
            <script>
                new Vue({
                    el: '#app',
                    data: {
                        getNum:0,
                        str:''
                    }
                })
            </script>
    </body>
    ```

    > 修饰符支持链式写法即:` v-model.number.lazy='getNum'`	

    - `.trim`的使用
      - 语法 :  `v-model.trim='str'`
      - 数据的首位空格会被删除 . 

    ```html
        <body>
            <div id="app">
                <input type="number" v-model.number.lazy='getNum'>
                <!-- v-pre 所在标签不被编译 -->
                <h2 v-pre>{{getNum+1}}</h2>
                <input type="text" v-model.trim='str'>
                <pre v-once>{{str}}</pre>
                <pre>{{str}}</pre>
            </div>
            <script src="./lib/vue.js"></script>
            <script>
                new Vue({
                    el: '#app',
                    data: {
                        getNum:0,
                        str:'hello'
                    }
                })
            </script>
        </body>
    ```

- ### [v-cloak](https://cn.vuejs.org/v2/api/#v-cloak)

  - **不需要表达式**

  - **用法**：

    这个指令保持在元素上直到关联实例结束编译。在需要添加的Mustache 标签上像属性一样添加`v-cloak `, 和 CSS 规则如 `[v-cloak]{ display: none }` 一起用时，这个指令可以隐藏未编译的 Mustache 标签直到实例准备完毕。

  - **示例**：

    ```css
    [v-cloak] {
      display: none;
    }
    ```

    ```html
    <div v-cloak>
      {{ message }}
    </div>
    ```

    不会显示，直到编译结束。

- ### [v-pre](https://cn.vuejs.org/v2/api/#v-pre)

  - **不需要表达式**

  - **用法**：

    跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。

  - **示例**：

    ```html
    <span v-pre>{{ this will not be compiled }}</span>
    ```

- ### [v-once](https://cn.vuejs.org/v2/api/#v-once)

  - **不需要表达式**

  - **详细**：

    **只渲染元素和组件一次**。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。

    ```
    <!-- 单个元素 -->
    <span v-once>This will never change: {{msg}}</span>
    <!-- 有子元素 -->
    <div v-once>
      <h1>comment</h1>
      <p>{{msg}}</p>
    </div>
    <!-- 组件 -->
    <my-component v-once :comment="msg"></my-component>
    <!-- `v-for` 指令-->
    <ul>
      <li v-for="i in list" v-once>{{i}}</li>
    </ul>
    ```