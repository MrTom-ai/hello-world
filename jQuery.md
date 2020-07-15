# jQuery是JavaScript的类库

[jQuery的官网](www.jquery.com)

[jQuery API中文文档](https://jquery.cuishifeng.cn/ )

### 多库共存：

运行这个函数将变量$的控制权让渡给第一个实现它的那个库。这有助于确保jQuery不会与其他库的$对象发生冲突。 在运行这个函数后，就只能使用jQuery变量访问jQuery对象。例如，在要用到$("div p")的地方，就必须换成jQuery("div p")。 '''注意:'''这个函数必须在你导入jQuery文件之后，并且在导入另一个导致冲突的库'''之前'''使用。当然也应当在其他冲突的库被使用之前，除非jQuery是最后一个导入的。

`jQuery.noConflict([extreme])`

#### **extreme**  Boolean   *V1.0*

传入 true 来允许彻底将jQuery变量还原

#### 描述:

将$引用的对象映射回原始的对象。

##### jQuery 代码:

```js
jQuery.noConflict();
// 使用 jQuery
jQuery("div p").hide();
// 使用其他库的 $()
$("content").style.display = 'none';
```

#### 描述:

恢复使用别名$，然后创建并执行一个函数，在这个函数的作用域中仍然将$作为jQuery的别名来使用。在这个函数中，原来的$对象是无效的。这个函数对于大多数不依赖于其他库的插件都十分有效。

##### jQuery 代码:

```js
jQuery.noConflict();
(function($) { 
  $(function() {
    // 使用 $ 作为 jQuery 别名的代码
  });
})(jQuery);
// 其他用 $ 作为别名的库的代码
```

#### 描述:

创建一个新的别名用以在接下来的库中使用jQuery对象。

##### jQuery 代码:

```js
var j = jQuery.noConflict();
// 基于 jQuery 的代码
j("div p").hide();
// 基于其他库的 $() 代码
$("content").style.display = 'none';
```

#### 描述:

完全将 jQuery 移到一个新的命名空间。

##### jQuery 代码:

```
var dom = {};
dom.query = jQuery.noConflict(true);
```

##### 结果:

```
// 新 jQuery 的代码
dom.query("div p").hide();
// 另一个库 $() 的代码
$("content").style.display = 'none';
// 另一个版本 jQuery 的代码
jQuery("div > p").hide();
```

### 文档就绪：

## ready(fn)

### 概述

当DOM载入就绪可以查询及操纵时绑定一个要执行的函数。

这是事件模块中最重要的一个函数，因为它可以极大地提高web应用程序的响应速度。

简单地说，这个方法纯粹是对向window.load事件注册事件的替代方法。通过使用这个方法，可以在DOM载入就绪能够读取并操纵时立即调用你所绑定的函数，而99.99%的JavaScript函数都需要在那一刻执行。

有一个参数－－对jQuery函数的引用－－会传递到这个ready事件处理函数中。可以给这个参数任意起一个名字，并因此可以不再担心命名冲突而放心地使用$别名。

请确保在 <body> 元素的onload事件中没有注册函数，否则不会触发+$(document).ready()事件。

可以在同一个页面中无限次地使用$(document).ready()事件。其中注册的函数会按照（代码中的）先后顺序依次执行。

### 参数

#### **fn**  Function *V1.0*

要在DOM就绪时执行的函数

### 示例

#### 描述:

在DOM加载完成时运行的代码，可以这样写：

##### jQuery 代码:

```
$(document).ready(function(){
  // 在这里写你的代码...
});
```

#### 描述:

使用 $(document).ready() 的简写，同时内部的 jQuery 代码依然使用 $ 作为别名，而不管全局的 $ 为何。

##### jQuery 代码:

```
$(function($) {
  // 你可以在这里继续使用$作为别名...
});
```

## jquery事件

#### blur([[data],fn])

### 概述

当元素失去焦点时触发 blur 事件。

这个函数会调用执行绑定到blur事件的所有函数，包括浏览器的默认行为。可以通过返回false来防止触发浏览器的默认行为。blur事件会在元素失去焦点的时候触发，既可以是鼠标行为，也可以是按tab键离开的

### 参数

#### **fn**Function*V1.0*

在每一个匹配元素的blur事件中绑定的处理函数。

#### **[data],fn**String,Function*V1.4.3*

**data**:blur([Data], fn) 可传入data供函数fn处理。

**fn**:在每一个匹配元素的blur事件中绑定的处理函数。

### 示例

#### 描述:

触发所有段落的blur事件

##### jQuery 代码:

```
$("p").blur();
```

#### 描述:

任何段落失去焦点时弹出一个 "Hello World!"在每一个匹配元素的blur事件中绑定的处理函数。

##### jQuery 代码:

```
$("p").blur( function () { alert("Hello World!"); } );
```
## 选择器

## 事件

### 事件委托

## class操作

## 文本内容

## 动画效果

## DOM

## jquery插件开发

## ajax