# [v-on](https://cn.vuejs.org/v2/api/#v-on)

- **缩写**：`@`
- **所需要的的类型**：`Function | Inline Statement | Object`
- **参数**：`event`
- 支持所有的原生`JS`事件，**事件类型前的`on`不可以添加**
- 支持动态事件 `v-on:[clicktype]='btnClick'` 方括号中变量名称必须使用小写。
- 有时也需要在内联语句处理器中访问原始的 DOM 事件。可以用特殊变量 `$event` 把它传入方法 . 

使用`v-on`时，需要在事件所在的组件中添加`methods`对象，对象里面放置的是事件触发时所使用的函数，`v-on`使用时是在需要触发事件的节点中添加`v-on:'事件类型=函数名'`，根据事件节点所对应的组件中写入对象`methods`,在`methods`写入上述事件的函数，函数名为`v-on`所定义的函数名。使用缩写时将`v-on：`换成`@`。

举个栗子：

```html
<body>
    <div id="app">
        <input type="text" v-model='msg' v-on:change='inputChange' />
        <!--<input type="text" v-model='msg' @change='inputChange' />-->
        <h2>{{msg}}</h2>
        <h3>{{num}}</h3>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        new Vue({
            el:"#app",
            data:{
                msg:'',
                num:1,
            },
            methods:{
                inputChange(){
                    this.num += 1
                }
            }
        })
    </script>
</body>
```

根据需要可以写成内联式的，如下面栗子：

```html
<body>
    <div id="app">
        <input type="text" v-model='msg' v-on:input = inputChange(msg) />
        <!--<input type="text" v-model='msg' @input = inputChange(msg) />-->
        <h2>{{msg}}</h2>
        <h2>{{num}}</h2>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        new Vue({
            el:"#app",
            data:{
                msg:'',
                num:0,
                args:[]
            },
            methods:{
                inputChange(text){
                    this.args = text.split('')
                    this.num = this.args.length
                    if(this.args.length>10){
                        this.num = this.args.length = 10
                        this.msg=this.args.join('')
                    }
                    }
                },
            }
        )
    </script>
</body>
```

也可以使用写成对象的形式，不过不建议使用。

## `v-on`的常用修饰符

`.stop`调用 `event.stopPropagation()` , 阻止事件冒泡  :

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .box{
            color: #fff;
        }
    </style>
</head>
<body>
    <div id="app">
        <div @click=colorClick>
            <div :style=[a1]  :class="{box:num == 1}" @click.stop=huiXiang >我变色了</div>
            <div :style=[a2] :class="{box:num == 2}" @click=huiXiang>我变色了</div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        new Vue({
            el:"#app",
            data:{
                a1:{
                    width:'100px',
                    height:'100px',
                    background:'red',
                    cursor: 'pointer',
                    userSelect: 'none'
                },
                a2:{
                    width:'200px',
                    height:'100px',
                    background:'blue',
                    cursor: 'pointer',
                    userSelect: 'none'
                },
                num:1
            },
            methods:{
                colorClick(ev){
                    if(1 == this.num){
                        this.num = 2
                    }else{
                        this.num = 1
                    }
                    console.log(ev.target)
                },
                huiXiang(ev){
                    console.log(ev.target)
                }
            }
        })
    </script>
</body>
</html>
```

`.self`拥有事件的节点会被触发 , 不会有事件冒泡和事件捕获  :

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
    <style>
        .box{
            color: #fff;
        }
    </style>
</head>
<body>
    <div id="app">
        <div @click.self =colorClick>
            <div :style=[a1]  :class="{box:num == 1}">我变色了</div>
            <div :style=[a2] :class="{box:num == 2}">我变色了</div>
        </div>
    </div>
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <script>
        new Vue({
            el:"#app",
            data:{
                a1:{
                    width:'100px',
                    height:'100px',
                    background:'red',
                    cursor: 'pointer',
                    userSelect: 'none'
                },
                a2:{
                    width:'200px',
                    height:'100px',
                    background:'blue',
                    cursor: 'pointer',
                    userSelect: 'none'
                },
                num:1
            },
            methods:{
                colorClick(ev){
                    if(1 == this.num){
                        this.num = 2
                    }else{
                        this.num = 1
                    }
                    
                },
                huiXiang(ev){
                    console.log(ev.target)
                }
            }
        })
    </script>
</body>
</html>
```

`.prevent` 与事件 `event.preventDefault()` , 阻止默认事件。

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <div class="dropBox" :style="{height:'200px',border:'1px solid gray'}" 
        @dragover.prevent = imgDragOver @drop.prevent = imgDrop ></div>

        <img :src=imgSrc :style="{width:'200px',height:'auto'}" />
    </div>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:"#app",
            data:{
                imgSrc:"",
            },
            methods: {
                imgDragOver(){},
                imgDrop(ev){
                    let This = this.$data
                    let fs = ev.dataTransfer.files
                    let fd = new FileReader()
                    fd.readAsDataURL(fs[0])
                    fd.onload = function(){
                        This.imgSrc = this.result
                                         
                    }
                }
            },
        })
    </script>
</body>
</html>
```

`.once` - 只触发一次回调。

```html
<body>
    <div id="root">
        <h2>{{num}}</h2>
        <button @click.once=onceClick>只能点击一次</button>
    </div>
    <script src="./vue.js"></script>
    <script>
        new Vue({
            el:'#root',
            data:{
                num:0
            },
            methods: {
                onceClick(){
                    this.num++
                }    
            },
        })
    </script>
</body>
```

 [详细内容复制链接](https://cn.vuejs.org/v2/guide/events.html)