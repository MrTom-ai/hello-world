#AJAX
##一，AsynchronousJavaScript+XML（异步JavaScript和XML）
1. 由来：在 Ajax 出现之前页面上数据发生改变的话就需要重新加载整个页面。而 Ajax 可以只对内容变化的区域进行数据的更新。使用Ajax可以减少与服务器数据的交互，从而提高效率，改善用户体验。
2. 尽管“X”在Ajax中代表XML, 但由于JSON的许多优势，比如更加轻量以及作为Javascript的一部分，目前JSON的使用比XML更加普遍。JSON和XML都被用于在Ajax模型中打包信息。（数据格式较早时候是用XML格式打包，现在是使用JSON格式打包）
##二，协议
  1. TCP/IP：TCP，约束数据如何传递；IP，IP地址相当于计算机的“身份证”。是计算机的唯一标识。

  2. 约束软件的端口号（0-65535,0-1023系统占用，1024-65535 ；如果端口号是80，在浏览器地址栏可以不用输入）

  3. 在window下 查看IP时使用cmd命令输入“ipconfig”，在Linux下查看IP时使用ifconfig。

  4. 域名映射：域名映射即域名反向解析，即从IP地址到域名的映射。由于在域名系统中，一个IP地址可以对应多个域名，因此从IP出发去找域名，理论上应该遍历整个域名树，但这在Internet上是不现实的。

     为了完成逆向域名解析，系统提供一个特别域，该特别域称为逆向解析域。这样欲解析的IP地址就会被表达成一种像域名一样的可显示串形式，后缀以逆向解析域域名结尾。

     两种表达方式中IP地址部分顺序恰好相反，因为域名结构是自底向上（从子域到域），而IP地址结构是自顶向下（从网络到主机）的。实质上逆向域名解析是将IP地址表达成一个域名，以地址做为索引的域名空间，这样逆向解析的很大部分可以纳入正向解析中。
###HTTP
1. 超文本传输协议（HTTP）是一个用于传输超媒体文档（例如 HTML）的应用层协议。它是为 Web 浏览器与 Web 服务器之间的通信而设计的，但也可以用于其他目的。HTTP 遵循经典的客户端-服务端模型，客户端打开一个连接以发出请求，然后等待它收到服务器端响应。
2. **HTTP 是无状态协议，这意味着服务器不会在两个请求之间保留任何数据（状态）。**该协议虽然通常基于 TCP/IP 层，但可以在任何可靠的传输层上使用；也就是说，不像 UDP，**它是一个不会静默丢失消息的协议**。
3. HTTP (The HyperText Transfer Protocol，超文本传输协议) 是用于在 Web 上传输超媒体文件的底层协议 ，最典型场景的是在浏览器和服务器之间传递数据，以供人们浏览。现行的 HTTP 标准的版本是 HTTP/2。
4. “http://” 称为 “schema”，是 URI 的组成部分，一般位于网络地址的开头。以“https://developer.mozilla.org”为例，该地址说明请求文档时使用“ HTTP 协议；这里的 https 代指 HTTP 协议的安全版本，即 SSL （或称 TLS）
5. HTTP 是基于文本的(所有的通信都以纯文本的形式进行) 以及无状态的 (当前通信状态不会发现以前的通信状态)，该特性极大方便了在www上浏览网页的人。除此之外，HTTP也可以用于构建服务器之间交互的 REST web 服务，以及使得网站内容更加动态化的 AJAX 请求。

## 三，域名系统概述

**域名系统DNS(Domain Name System)**是因特网使用的命名系统，用来把便于人们使用的机器名字转换成为IP地址。域名系统其实就是名字系统。为什么不叫“名字”而叫“域名”呢？这是因为在这种因特网的命名系统中使用了许多的“域(domain)”，因此就出现了“域名”这个名词。“域名系统”明确地指明这种系统是应用在因特网中。

IP地址是由32位的二进制数字组成的。用户与因特网上某台主机通信时，显然不愿意使用很难记忆的长达32位的二进制主机地址。即使是点分十进制IP地址也并不太容易记忆。相反，大家愿意使用比较容易记忆的主机名字。**但是，机器在处理IP数据报时，并不是使用域名而是使用IP地址。**这是因为IP地址长度固定，而域名的长度不固定，机器处理起来比较困难。

因为因特网规模很大，所以整个因特网只使用一个域名服务器是不可行的。因此，早在1983年因特网开始采用层次树状结构的命名方法，并使用分布式的域名系统DNS。并采用客户服务器方式。DNS使大多数名字都在本地解析(resolve)，仅有少量解析需要在因特网上通信，因此DNS系统的效率很高。由于DNS是分布式系统，即使单个计算机除了故障，也不会妨碍整个DNS系统的正常运行。

**域名到IP地址的解析是由分布在因特网上的许多域名服务器程序共同完成的。**域名服务器程序在专设的结点上运行，而人们也常把运行域名服务器程序的机器称为域名服务器。

域名到IP地址的解析过程的要点如下：

1. 当某一个应用需要把主机名解析为IP地址时，该应用进程就调用解析程序，并称为DNS的一个客户，把待解析的域名放在DNS请求报文中，以UDP用户数据报方式发给本地域名服务器。
2. 本地域名服务器在查找域名后，把对应的IP地址放在回答报文中返回。应用程序获得目的主机的IP地址后即可进行通信。
3. 若本地域名服务器不能回答该请求，则此域名服务器就暂时称为DNS的另一个客户，并向其他域名服务器发出查询请求。

![域名解析](.\img\域名解析.jpg)



###HTTP请求方法

**GET**(重点)

- GET方法请求一个指定资源的表示形式. 使用GET的请求应该只被用于获取数据.

**HEAD**

- HEAD方法请求一个与GET请求的响应相同的响应，但没有响应体.

**POST**(重点)

- POST方法用于将实体提交到指定的资源，通常导致在服务器上的状态变化或副作用.

**PUT**(重点)

- PUT方法用请求有效载荷替换目标资源的所有当前表示。

**DELETE**

- DELETE方法删除指定的资源。

**CONNECT**

- CONNECT方法建立一个到由目标资源标识的服务器的隧道。

**OPTIONS**

- OPTIONS方法用于描述目标资源的通信选项。

**TRACE**

- TRACE方法沿着到目标资源的路径执行一个消息环回测试。

**PATCH**

- PATCH方法用于对资源应用部分修改。

### HTTP状态码

HTTP 响应状态代码指示特定 HTTP 请求是否已成功完成。**响应分为五类：信息响应(100–199)，成功响应(200–299)，重定向(300–399)，客户端错误(400–499)和服务器错误 (500–599)。** [HTTP状态码表](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Status)

>###200 OK
>请求成功。成功的含义取决于HTTP方法：
GET：资源已被提取并在消息正文中传输。
HEAD：实体标头位于消息正文中。
POST：描述动作结果的资源在消息体中传输。
TRACE：消息正文包含服务器收到的请求消息。
>###400 Bad Request
1、语义有误，当前请求无法被服务器理解。除非进行修改，否则客户端不应该重复提交这个请求。
>404 Not Found：
请求失败，请求所希望得到的资源未被在服务器上发现。没有信息能够告诉用户这个状况到底是暂时的还是永久的。假如服务器知道情况的话，应当使用410状态码来告知旧资源因为某些内部的配置机制问题，已经永久的不可用，而且没有任何可以跳转的地址。404这个状态码被广泛应用于当服务器不想揭示到底为何请求被拒绝或者没有其他适合的响应可用的情况下。

## 四，AJAX 的基本使用

#### 编写一个ajax请求分为四部（重要）

- **创建请求对象**
- **设置请求参数**
- **发送请求**
- **接收响应数据**

1. 创建 Ajax 请求对象:`XMLHttpRequest` 

```js
// 1. 创建 ajax 请求对象。
var xhr = null;
if (window.XMLHttpRequest) {
    xhr = new XMLHttpRequest();
}else{
    // 兼容 IE5/6
    xhr = new ActiveXObject("Microsoft.XMLHTTP")
}
```

2. 设置请求参数: `xhr.open()`使用 open()设置请求参数，该函数有三个参数：

   - 参数1：请求方式POST/GET。
   - 参数2：请求的地址URL。
   - 参数3：是否异步请求,true/false。设置为false时为同步程序将会阻塞，不建议使用。

   2. 1.get请求示例：

```js
xhr.open("get", "/ajax/server.php?name=小明&age=19", true);
```

> get请求的参数直接跟在URL后面。

​	   2 . 2 .post请求示例： 

```js
xhr.open("post", "/ajax/server.php", true);
//设置请求头
xhr.setRequestHeader("Content-type","application/x-www-form-urlencoded");
//  提交给服务器，并且设置请求参数。
xhr.send("name=小明&age=19");
```



> post 请求必须要设置请求头，请求参数在提交给服务器的send()函数中设置。 媒体类型[媒体类型](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Basics_of_HTTP/MIME_types) Content-type取值参考 [media-types](https://www.iana.org/assignments/media-types/media-types.xhtml#application)  
>
> `setRequestHeader()`设置HTTP请求头部的方法 ，您必须在 open() 之后、send() 之前调用 setRequestHeader() 方法。  

3. 将请求提交给服务器:`xhr.send()` 

```js
xhr.send("name=小明&age=19");
```

> 在send()的参数中可以设置请求要传递给服务器的数据。要注意，该参数只有在POST请求时才有效。 
>
> get或者是post请求参数中如果有特殊字符如:"& \ % = "可以使用编码函数与解码函数escape(String s)和unescape(String s) 对请求参数进行编码的转换。 

4. 等待服务器响应:`xhr.onreadystatechange()` 

```js
xhr.onreadystatechange = function () {
    if (4 == xhr.readyState &&　200 == xhr.status) {
        alert(xhr.responseText);
    }
}
```

- xhr.readyState：
  - **0**: 请求未初始化
  - **1**: 服务器连接已建立
  - **2**: 请求已接收
  - **3**: 请求处理中
  - **4**: 请求已完成，且响应已就绪

- xhr.status: HTTP状态码
- xhr.responseText: 字符串格式的响应内容。
- [XMLHttpRequest常用属性及方法](https://developer.mozilla.org/zh-CN/docs/Web/API/XMLHttpRequest) 

### 运行环境

[phpStudy下载](http://192.168.6.164/sppt/study/ajax/PhpStudy20180211.zip) 

- phpStudy 是一款集成的服务器端环境，解压后可直接使用
- 解压路径中不能包含空格和中文

> 编写的 **ajax**代码需要在服务器环境下运行 

- 如果请求的文件是 `.json`文件 需要注意只能使用 **get**请求方式 

## 五，基于 promise ajax的封装

```js
/**
 * ajax
 * @param {Object} args 
 * args.url 请求路径
 * args.method 请求方式，可选的
 * args.data 请求数据,json格式{}，可选的
 */

function ajax(args) {
    if (!args.method) {
        args.method = "get"
    }
    const promise = new Promise(function (resolve, reject) {
        let xhr = null;
        if (window.XMLHttpRequest) {
            xhr = new XMLHttpRequest();
        } else {
            xhr = new ActiveXObject("Microsoft.XMLHTTP")
        }
        let oData = new FormData();
        for (const key in args.data) {
            oData.append(key, args.data[key])
        }
        xhr.open(args.method, args.url, true);
        xhr.send(oData);
        xhr.onreadystatechange = function () {
            if (4 == xhr.readyState && 200 == xhr.status) {
                try {
                    switch (args.method) {
                        case "head":
                        case "Head":
                            return resolve({
                                statusText: this.statusText,
                                status: this.status,
                                url: this.responseURL,
                                readyState: this.readyState
                            })
                        default:
                           return resolve(JSON.parse(this.response))
                    }
                    
                } catch (error) {
                    resolve(this.response)
                }

            } else if (4 == xhr.readyState) {
                reject(new Error(xhr.status));
            }
        }
    })

    return promise;

}
```

