# Client_JS  
  
  
### 作者：冰红茶  
### 参考书籍：《JavaScript权威指南》第二部分   

------    



   最开始的时候看完了《javascript权威指南》的第一部分，然后准备进入第二部分客户端JS的学习的时候，发现很多东西都是需要跟HTML和CSS的知识是在几个月前看第一轮学习中从入门到精通系列学的，感觉学得很粗糙，知识体系没有完全建立起来。遂果断进入二轮恶补阶段，把CSS和HTML5权威指南看来一遍，然后又把张老师的CSS世界补完，算是有了基本的知识体系。现在，就是进入《javascript权威指南》的第二部分的时候了^_ ^
  
## 目录

## [一、Web浏览器的JavaStript](#1)
### [1.1 Web文档中的JS](#1.1)
### [1.2 在HTML中嵌入JS](#1.2) 
### [1.3 时间线与同步、异步和延迟](#1.3) 
### [1.4 兼容性和互用性](#1.4)
### [1.5 安全性](#1.5)
## [二、Window对象](#2)
### [2.1 属性](#2.1)
### [2.2 计时器](#2.2) 
### [2.3 对话框](#2.3)
### [2.4 错误处理onerror](#2.4)
### [2.5 多窗口和窗体](#2.5)
## [三、脚本化文档](#3)
### [3.1 DOM概览](#3.1)
### [3.2 选取文档元素](#3.2)
### [3.3 文档结构和遍历](#3.3)
### [3.4 属性](#3.4)
### [3.5 元素的内容](#3.5)
### [3.6 元素操纵方法](#3.6)
### [3.7 document.write()](#3.7)
### [3.8 文档和元素的几何形状和滚动](#3.8)
## [四、事件处理](#4)
### [4.1 简介](#4.1)
### [4.2 事件类型](#4.2) 
### [4.3 注册事件处理程序](#4.3)
### [4.4 循环绑定事件](#4.4)
### [4.5 事件处理程序的调用](#4.5)
### [4.6 文档加载事件](#4.6)
### [4.7 几种页面跳转的方法](#4.7)		  
## [五、脚本化CSS](#5)
### [5.1 脚本化内联样式](#5.1)
### [5.2 脚本化CSS类](#5.2) 
### [5.3 脚本化样式表](#5.3) 
## [六、脚本化HTTP](#6)
### [6.1 Ajax和Comet](#6.1)
### [6.2 XMLHttpRequest](#6.2) 
### [6.3 编码请求主体](#6.3)      
### [6.4 HTTP进度事件](#6.4)
### [6.5 跨域请求](#6.5)
## [七、客户端储存](#7)
### [7.1 客户端储存简介](#7.1)
### [7.2 localStorage和sessionStorage](#7.2) 
### [7.3 cookie](#7.3)      
### [7.4 应用程存储和离线Web应用](#7.4)
## [八、HTML5 API](#8)
### [8.1 地理位置](#8.1)
### [8.2 历史记录管理](#8.2) 
### [8.3 跨域消息传递](#8.3)      
### [8.4 Web Worker](#8.4)
### [8.5 类型化数组和ArrayBuffer](#8.5)
### [8.6 Blob](#8.6) 
### [8.7 文件系统API](#8.7)      
### [8.8 客户端数据库](#8.8)
### [8.9 Web套接字](#8.9)
## [附件](#10)
### [1、遍历样式表结果](#10.1)
### [2、HTTP状态码列表](#10.2) 
### [3、permanote.js](#10.3)   
------ 		
        

<h2 id='1'> 一、Web浏览器的JavaStript </h2>
<h3 id='1.1'>1.1 Web文档中的JS</h3>  

#### 1) [global对象、Windows对象和document对象](https://blog.csdn.net/summer_15/article/details/73255115) 
> - Window对象是所有客户端JS特性和API的主要接入点，它表示Web浏览器的一个窗口或者窗体，并且可以用标识符window来引用它；
> - window对象是宿主对象也就是在一定的环境中才会生成的对象（这里也就是指浏览器），而global对象是在任何环境中都存在的。window对象具体也就是指浏览器打开的那个窗口；
> - document对象是window对象的一个属性，是显示于窗口内的一个文档。而window对象则是一个顶层对象，它不是另一个对象的属性。document可以理解为文档，就是你的网页，而window是你的窗口，就是你的浏览器包含的。它们俩在没有框架的情况下可以说是等同的，在有框架的情况下就要区别对待了。
#### 2) 脚本类型  
> - javascript
> - VBScript 巨硬公司IE专用的，MIME类型必须是type="text/vbscript";

<h3 id='1.2'>1.2 在HTML中嵌入JS</h3>  

#### 1) 在HTML中嵌入JS  
> - 内联，直接放在script的标签之间；
> - 从外部引入，利用script中的src属性，此时标签中间的代码无效化，但是可以添加一些注释和关于脚本的信息；
> - 在事件处理程序onclick()、onmousemove()这样的HTML属性指定；
> - 在URL中添加“javascript:我是代码”    
  
#### 2) “javascript:我是代码”  
> - 利用的是“javascript:”协议
> - 注释必须使用/\*注释\*/
> - 利用的是“javascript:我是代码”中返回的值，如果不返回值的话，最好使用void操作符,
        
                href = "javascript: ;"
                或者
                href = "javascript: void(0);"
> - 否则有的返回值会被转化为字符串显示\[object Window\]
> - Web早期的产物，现在最好不要使用；
> - 应用:书签程序


<h3 id='1.3'>1.3 客户端JS的线程模型</h3>   

#### 1) 单线程  
> - 避免锁，死锁和竞争条件；
#### 2) Web worker  
> - HTML5定义的一种并发控制方式；
> - 不能访问文档内容，不能与其他侠worker或者主线程共享状态；
> - 只可以和主线程和其他worker通过异步事件通讯，所以不能检查并发性；
#### 3) 客户端JS的时间线 
    
>> 次序|动作|readystate属性|能否使用document.write()   
>> -|-|-|-
>> 1|创建document对象，开始解析HTML文档|loading|
>> 2|默认的时候同步下载JS脚本文件|loading|能
>> 3|异步则继续解析文档|loading|不能
>> 4|当文档解析完|interactive|-
>> 5|所有的defer脚本会在文档里按顺序执行，异步脚本则有可能执行|-|异步则不能
>> 6|document对象触发DOMContentLoaded事件，标志着程序执行从同步脚本执行阶段切换到异步事件驱动阶段，但是需要注意的是异步脚本没有执行完成|-|-
>> 7|文档完全解析完成，但浏览器还在等待相关资源的载入，如图片，还有异步脚本还在执行|当所有资源载入和所有异步脚本执行完毕后，complete，Web浏览器触发Windows对象上的load事件|-
>> 8|调用异步事件，以异步相应客户的输入|-|-   

> - 这是一个非常理想的时间线，DOMContentLoaded事件在load时间之前触发

<h3 id='1.4'>1.4 兼容性和互用性</h3>   

#### 1) 问题总结  
> - 演化——新老浏览器之间的不兼容 随着标准规范的更新，一些新的浏览器会支持，一些老的不支持，需要在老浏览器的大群体和新浏览器的小群体中做出权衡
> - 未实现——各家浏览器之间的不兼容 对于某个特性，各家浏览器实现的情况都不一样。
> - bug 每个浏览器都有bug    

#### 2) 兼容性框架——jQuery  
> - 事件处理程序的注册是通过叫bind()的方法完成的，不用担心和考虑addEventListener（这是JavaStript的函数）和attachEvent()（这是VBStript的函数）之间的不兼容性问题。
#### 3) 分级浏览器 
> - 起初是Yahoo！率先提出的一种测试技术，从某个维度对浏览器厂商/版本/操作系统进行分级。分级浏览器中的A级要通过所有功能测试用例，C级则不必通过所有。
#### 4) 怪异模式和标准模式 
> - 标准模式则需要兼容CSS标准规范 document.compatMode==CSS1Compat
> - 怪异模式则需要遵循浏览器自己的规范（这主要是为了兼容老版本的浏览器） document.compatMode==BackCompat/undefined

<h3 id='1.5'>1.5 安全性</h3>   

#### 1) JS不能做什么  
> - 不支持对用户文件进行访问和修改
> - 没有通用的网络能力
>> - 只有用户点击确认才能打开新的浏览器窗口（防止广告弹窗）
>> - 只能关闭自己的窗口，不能关闭其他的浏览器窗口
>> - 上传文件的value属性只读
>> - 脚本不能读取来自不同浏览器载入的文档内容（同源策略）
#### 2) 同源策略
> - 何为同源：采用相同的协议 主机 端口
> - 脚本只能读取和所属文档来源相同的窗口和文档，或者说脚本只能对直接文档起作用，对间接文档不能访问
#### 3) 不严格的同源策略
> - 默认情况下document的domain属性存放的是载入文档的服务器的主机名，如果两个窗口或者窗体的脚本的domain属性设置成相同的值，则不受同源策略的约束；
> - 跨域资源共享Crossing-Origin Resource Sharing 它允许服务器用头信息显示地列出源，或者使用通配符来匹配所有的源并允许其访问。请求头是Origin，相应头是Access-Control-Allow-Origin，这样XMLHttpRequest就不受同源的约束了
> - 跨文档消息 允许来自一个文档的脚本可以传递文本消息到另一个文档的脚本，而不管脚本是否同源。调用的是Windows对象上的postMessage()方法，异步传递消息。但是还是不能调用其他文档的方法和读取里面的属性，一次以此实现安全的通讯。
#### 4) 跨站脚本
> - 在URL地址上添加脚本
#### 5) 拒绝服务攻击
        
------
        
<h2 id='2'> 二 Window对象 </h2>    
<h3 id='2.1'>2.1 属性</h3>  
  
>> Window属性|Window属性|方法
>> -|-|-
>> Window.location|Location对象|asign()/replace()/reload()
>> Window.history|History对象|back()和forward()
>> Window.navigator|Navigator对象|引用包含浏览器厂商和版本信息
>> Window.screen|Screen对象|有关窗口显示的大小和可用颜色数量的信息 
		
>> - Document也有一个URL属性，是文档首次载入时保存该文档的URL静态字符串，Location对象的href属性（当前文档的URL的完整文本的字符串）可以改变，但是Document.URL首次载入后就不能改变。
>> - Location对象的href属性保存当前文档的URL的完整文本的字符串，可以使用Location.toString()方法返回href属性的值，同时也可以隐式调用。调用的时候便可替代Location.href；
>> - Location的assign(URL)表示使窗口载入并显示你指定的URL中的文档。replace()方法也类似，但它载入的时候会将浏览历史中的它的记录删除；
>> - history back()和forward()方法只接受一个数字类型作为参数，可以是负数，表示前进或者返回第n个页面。如：
		
        		history.go(-2);			
        		//后退两个历史记录，相当于单击“后退”按钮两次			
>> - location对象
>>>>>> ![图3-11 location对象](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-11%20location%E5%AF%B9%E8%B1%A1.png?raw=true)
>> - document对象
>>>>>> ![图3-9 document对象A](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-9%20document%E5%AF%B9%E8%B1%A1A.png?raw=true)  
>>>>>> ![图3-10 document对象B](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-10%20document%E5%AF%B9%E8%B1%A1B.png?raw=true)  
>> -  Window对象
>>>>>> ![图3-12 Window对象a](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-12%20Window%E5%AF%B9%E8%B1%A1a.png?raw=true)  
>>>>>> ![图3-12 Window对象b](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-12%20Window%E5%AF%B9%E8%B1%A1b.png?raw=true)		
>> -  History对象
>>>>>> ![图3-13 History对象](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-13%20History%E5%AF%B9%E8%B1%A1.png?raw=true)  
>> -  Screen对象
>>>>>> ![图3-14 Screen对象.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE3-14%20Screen%E5%AF%B9%E8%B1%A1.png?raw=true)  


<h3 id='2.2'>2.2 计时器</h3>  

#### 1) setTimeout(function, delaytime)
#### 2) setTimeout(function, delaytime, arguments)
> - setTimeout(code, milliseconds, param1, param2, ...)
> - setTimeout(function, milliseconds, param1, param2, ...)
> - 这个arguments参数是function的参数，可选。 传给执行函数的其他参数（IE9 及其更早版本不支持该参数）。
> - 返回一个 ID（数字），可以将这个ID传递给 clearTimeout() 来取消执行。
        
                var stopSignal = setTimeout(function(value) {console.log(value)}, 1000, "Hello!");
                console.log(stopSignal);
                var stop = function(stopSignal) {
                    clearTimeout(stopSignal);
                }; 

                09:59:44.653 VM2443:2 225664
                09:59:44.659 undefined
                09:59:45.655 VM2443:1 Hello!
#### 2) setInterval(function, repeattime)
#### 3) 如果需要终止，需利用返回的值作为clearTimeout的参数
>>>>>> ![图2-2 定时器应用函数](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE2-2%20%E5%AE%9A%E6%97%B6%E5%99%A8%E5%BA%94%E7%94%A8%E5%87%BD%E6%95%B0.png?raw=true)     

<h3 id='2.3'>2.3 对话框</h3>  

#### 1) prompt() 
>> - 获取输入对话框，需要用户输入后选择确认。会产生阻塞。
        
                我的名字：<span id="myName"></span>
                <script type="text/javascript">
                    var name = prompt("What is your name?");
                    document.getElementById("myName").innerHTML=name;
                </script>
#### 2) confirm() 
>> - 确认对话框，需要用户点击确认。会产生阻塞。
#### 3) alert() 
>> - 警告对话框，需要用户点击关闭。会产生阻塞。
#### 4) 模态对话框showModalDialog() 
>>>>>> ![图2-1 模态对话框showModalDialog()](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE2-1%20%E6%A8%A1%E6%80%81%E5%AF%B9%E8%AF%9D%E6%A1%86showModalDialog.png?raw=true)   


<h3 id='2.4'>2.4 错误处理onerror</h3>  

#### 1) onerror()三个参数
>> - window.onerror(description, URL, Line)
>>>>>> ![图2-3 错误处理](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE2-3%20%E9%94%99%E8%AF%AF%E5%A4%84%E7%90%86.png?raw=true)    

<h3 id='2.5'>2.5 多窗口和窗体</h3>  

#### 1) 子窗口和子窗体的区别：
>> - 子窗口指的是使用window.open打开的新的页面，双方不存在嵌套窗体的作用；
>> - 子窗体指的是窗口内通过iframe元素嵌套着的小窗体；
  
#### 2) [global对象、Windows对象和document对象](https://blog.csdn.net/summer_15/article/details/73255115) 
>> - Window对象是所有客户端JS特性和API的主要接入点，它表示Web浏览器的一个窗口或者窗体，并且可以用标识符window来引用它。包括：窗口，标签页，iframe和框架
>> - indow对象是宿主对象也就是在一定的环境中才会生成的对象（这里也就是指浏览器），而global对象是在任何环境中都存在的。window对象具体也就是指浏览器打开的那个窗口；
>> - document对象是window对象的一个属性，是显示于窗口内的一个文档。而window对象则是一个顶层对象，它不是另一个对象的属性。document可以理解为文档，就是你的网页，而window是你的窗口，就是你的浏览器包含的。它们俩在没有框架的情况下可以说是等同的，在有框架的情况下就要区别对待了。   

#### 3) id属性
>> - 必须是唯一的
>> - 元素的id属性为脚本可访问的全局变量；
>> - 但是不能与已有的关键字重复，否则无效，比如history,navigator, screen等    

#### 4) 标签页
>> - 理论上讲每个标签页都是独立的“浏览器上下文”（browsing content），每个上下文都有独立的Window对象，互相互不干扰。
>> - 虽然Window对象相互独立，但是不代表窗口之间也是相互独立。当一个标签页或者一个窗口是由另一个标签页或者窗口的脚本打开的时候，这样的窗口之间就可以互相操作了（但是也会受到同源策略的约束）
>> - 同样道理，嵌套的窗体之间也是可以互相看见的（但是也会受到同源策略的约束）
  
#### 5) [窗口的引用](http://javascript.ruanyifeng.com/bom/window.html#toc29) 
>> - top：顶层窗口，即最上层的那个窗口
>> - parent：父窗口
>> - self：当前窗口，即自身
    
                top === self  //下面代码可以判断，当前窗口是否为顶层窗口。   
                
                // 更好的写法
                window.top === window.self    
                
                parent.history.back();  //下面的代码让父窗口的访问历史后退一次。       
#### 6) [iframe标签——子窗体](http://javascript.ruanyifeng.com/bom/window.html#toc29) 
>> - 对于iframe嵌入的窗口，document.getElementById方法可以拿到该窗口的DOM节点，然后使用contentWindow属性获得iframe节点包含的window对象，或者使用contentDocument属性获得包含的document对象。
    
                var frame = document.getElementById('theFrame');
                var frameWindow = frame.contentWindow;

                // 等同于 frame.contentWindow.document
                var frameDoc = frame.contentDocument;

                // 获取子窗口的变量和属性
                frameWindow.function()

                // 获取子窗口的标题
                frameWindow.title   
>> - iframe元素遵守同源政策，只有当父页面与框架页面来自同一个域名，两者之间才可以用脚本通信，否则只有使用 *window.postMessage* 方法。iframe窗口内部，使用window.parent引用父窗口。如果当前页面没有父窗口，则window.parent属性返回自身。
        
                if (window.parent !== window.self) {
                  // 当前窗口是子窗口
                }       
>> - iframe嵌入窗口的window对象，有一个frameElement属性，返回它在父窗口中的DOM节点。对于那么非嵌入的窗口，该属性等于null。
        
                var f1Element = document.getElementById('f1');
                var fiWindow = f1Element.contentWindow;
                f1Window.frameElement === f1Element // true
                window.frameElement === null // 对于顶级窗口而言永远是true，因为它没有父窗口        
>> - 但是通常不需要搞得那么复杂，先要获取iframe元素，然后再通过该元素或者子窗体的的window对象。只要使用frame属性一步到位。frame属性是一个类数组对象，frame\[0\]表示所有嵌套子窗体排序的第一个。parent.frames\[1\]表示引用兄弟窗体。		
        
------		
                
<h2 id='3'> 三、脚本化文档 </h2>    
<h3 id='3.1'>3.1 DOM概览</h3>  
  	
#### 1) 相关概念
>> - DOM是表示和操作HTML和XML文档内容的基础API
>> - 祖先节点 父节点 子节点 兄弟节点 后代节点
>> - 文档Document又分HTMLDocument和XMLDocument，元素Element又分HTMLElement和XMLElement，两者是不一样的；
>> - document.body显式指代body标签；document.head显式指代head标签；document.documentElement显式指代根元素html；
>>>>>> ![图3-1 文档节点的部分层次结构](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-1%20%E6%96%87%E6%A1%A3%E8%8A%82%E7%82%B9%E7%9A%84%E9%83%A8%E5%88%86%E5%B1%82%E6%AC%A1%E7%BB%93%E6%9E%84.png?raw=true)  


<h3 id='3.2'>3.2 选取文档元素</h3>		
		
>>>>>> ![图3-16 寻找元素的Document方法](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-16%20%E5%AF%BB%E6%89%BE%E5%85%83%E7%B4%A0%E7%9A%84Document%E6%96%B9%E6%B3%95.png?raw=true) 		

#### 1) 通过ID属性选取
>> - getElementByID()		
#### 2) 通过name属性选取
>> - getElementsByName() 返回的是NodeList对象（按照文档出现的顺序进行排序），这是因为同名的元素可能不止一个；
>> - 名字name会自动加入到Document对象中并添加相应的属性；
>> - name的属性只出现在HTML中，XML没有
#### 3) 通过标签选取
>> - getElementsByTagName() 返回的是NodeList对象（按照文档出现的顺序进行排序），这是因为同名的元素可能不止一个；		
#### 4) 通过指定的CSS类选取
>> - getElementsByClassName() 返回的是NodeList对象（按照文档出现的顺序进行排序），这是因为同名的元素可能不止一个；对元素以及其子元素进行匹配；	
>> - 在HTML中，元素的类可以进行叠加，中间使用空格隔开。所以，在匹配的时候getElementsByClassName()的类名参数也可以用空格隔开，类名可以不按顺序；
>> - 怪异模式的出现是为了向后兼容（在文档的开头<!DOCTYPE>），class类名不区分大小写，如果在这种情况下，脚本的类名参数也不区分大小写，否则区分大小写；
>>>>>> ![图3-2 静态副本](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-2%20%E9%9D%99%E6%80%81%E5%89%AF%E6%9C%AC.png?raw=true) 
#### 5) 通过指定的CSS选择器选取
>> - querySelectorAll() 参数是CSS选择器的，返回的是匹配成功的NodeList对象；
>> - querySelector()参数是CSS选择器的，返回的是匹配成功的第一个对象；
>> - 对于伪类选择器，比如：link()或者：visited，很多浏览器会拒绝返回，因为可能会泄漏客户的浏览记录；
#### 6) document.all\[\]
>> - 出现在DOM标准化之前，现在已经弃用；
>>>>>> ![图3-3 document.all\[\]](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-3%20document.all%5B%5D.png?raw=true) 		

#### 7) NodeList和HTMLCollection的实时性
>> - HTMLCollection对象是document.images和document.forms的返回值
>> - NodeList和HTMLCollection对象都是只读的类数组对象，有length属性，可以按照数组那样使用编号进行索引，但不能直接调用Array的方法；
>> - 实时性即会跟据HTML和CSS的变化实时改变NodeList和HTMLCollection的返回值；
>> - 需要迭代进行添加或者删除元素的时候，需要建立一个副本
>>>>>> ![图3-2 静态副本](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-2%20%E9%9D%99%E6%80%81%E5%89%AF%E6%9C%AC.png?raw=true) 		
                        
<h3 id='3.3'>3.3 文档结构和遍历</h3>		
        
#### 1) 作为节点树的文档        
>> - 节点树主要包括Document对象，Element对象和Text对象都是Node对象
        
>> 次序|名字|含义   
>> -|-|-
>> 1|parentNode|父节点
>> 2|childNodes|子节点
>> 3|firstChild，lastChild|子节点的第一个和最后一个
>> 4|nextSibling，previousSibling|该节点的兄弟节点的前一个和后一个
>> 5|nodeType|返回节点的类型
>> 6|nodeValue|Text节点和Comment节点的文本内容
>> 7|nodeName|元素的标签名，以答谢的形式表示
>> 8|parentNode|父节点		

>> - nodeType返回值 9代表Document节点，1代表Element节点，3代表text节点，8代表Comment节点，11代表DocumentFragment节点；
>> - 用法：他的参考是Node对象，从Node对象出发：	
>>>>>> ![图3-4 作为节点树的文档](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-4%20%E4%BD%9C%E4%B8%BA%E8%8A%82%E7%82%B9%E6%A0%91%E7%9A%84%E6%96%87%E6%A1%A3.png?raw=true) 	
		
#### 2) 作为元素树的文档
>> - 主要额度研究兴趣点在文档的元素上而非它们之间的文本（和他们之间的空白，包括Text和Comment节点），参考点是具体的某个元素
        
>> 次序|名字|含义|返回   
>> -|-|-|-
>> 1|children|子节点|NodeList对象
>> 2|firstElementChild，lastElementChild|子元素的第一个和最后一个
>> 3|nextElementSibling，previousElementSibling|该元素的兄弟元素的前一个和后一个
>> 4|childElementCount|子元素的数量，返回值跟children.length的值相同		

>> - 说起奇怪，好像唯独是缺了parent，此时需要借助作为节点树的文档的parentNode。		
>>>>>> ![图3-5 返回元素e的第n层祖先元素](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-5%20%E8%BF%94%E5%9B%9E%E5%85%83%E7%B4%A0e%E7%9A%84%E7%AC%ACn%E5%B1%82%E7%A5%96%E5%85%88%E5%85%83%E7%B4%A0.png?raw=true)		

<h3 id='3.4'>3.4 属性</h3>		

#### 1) attribute VS proerty
>> - attributed代表的是元素的属性，名值对；
>> - proerty代表的是对象的属性；		
#### 2) HTML属性作为Element的属性
>> - 返回的类型基本与元素的属性的相同，而不是简单的额字符串
>> - HTML的属性是不区分大小写的，但是JS是区分的，所以在转化的过程中需要采用驼峰式的命名方式
>>>>>> ![图3-6 HTML属性作为Element的属性](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-6%20HTML%E5%B1%9E%E6%80%A7%E4%BD%9C%E4%B8%BAElement%E7%9A%84%E5%B1%9E%E6%80%A7.png?raw=true)		

#### 3) 获取和设置非标准的HTML属性
>> - 跟前面的API最大的区别是：返回的是字符串格式，其次，属性名采用标准属性名；
>> - html的属性不区分大小写；
>> - 方法包括getAttribute()；setAttribute()；hasAttribute()；removeAttribute()
>>>>>> ![图3-7 获取和设置非标准的HTML属性](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-7%20%E8%8E%B7%E5%8F%96%E5%92%8C%E8%AE%BE%E7%BD%AE%E9%9D%9E%E6%A0%87%E5%87%86%E7%9A%84HTML%E5%B1%9E%E6%80%A7.png?raw=true)		

#### 4) 作为Attr节点的属性
>> - 针对任何非Element对象的任何节点，该属性为null;
>> - 针对任何Element对象的任何节点，返回值是像NodeLists的类数组对象；
>>>>>> ![图3-8 作为Attr节点的属性](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-8%20%E4%BD%9C%E4%B8%BAAttr%E8%8A%82%E7%82%B9%E7%9A%84%E5%B1%9E%E6%80%A7.png?raw=true)			

<h3 id='3.5'> <a href="https://blog.csdn.net/debugingstudy/article/details/11100977">3.5 元素的内容</a></h3>		

        		<div id="test">     
        		   <span style="color:red">test1</span> test2     
        		</div> 		
#### 1) test.innerHTML（所有浏览器支持）：
        
                <span style="color:red">test1</span> test2
#### 2) test.outerHTML（所有浏览器支持）: 
>> - 除了包含innerHTML的全部内容外, 还包含对象标签本身。 
>> - 上例中的text.outerHTML的值也就是
        
                <div id="test"><span style="color:red">test1</span> test2</div> 
#### 3) test.innerText（IE仅支持）: 
>> - 从起始位置到终止位置的内容, 但它去除Html标签
>> - 上例中的text.innerTest的值也就是“test1 test2”, 其中span标签去除了。 
#### 4) test.textContent(除了IE都支持):
>> - 从起始位置到终止位置的内容, 但它去除Html标签
>> - 上例中的text.textContent的值也就是“test1 test2”, 其中span标签去除了。 所以同IE的innerText。
>> - 注意，要判断test.textContent在浏览器中是否兼容，不能直接使用
        
                if(test.textContent)，
>> - 这是因为假如test.textContent的值是一个空字符串，也会返回假值，所以最好是使用
        
                if(test.textContent === undefine )

<h3 id='3.6'>3.6 元素操纵方法</h3>		

#### 1) 新建添加删除复制
>>>>>> ![图3-17 DOM操纵成员](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-17%20DOM%E6%93%8D%E7%BA%B5%E6%88%90%E5%91%98.png?raw=true)
>>>>>> ![图3-17 DOM操纵成员b](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE3-17%20DOM%E6%93%8D%E7%BA%B5%E6%88%90%E5%91%98b.png?raw=true)
> - 新建节点creatElement()和增加节点appendChild()  appendChild()在最后一个子节点中插入
        
                /* 增加节点creatElement()
                 * 当contentbox高度增加的时候添加节点
                 */
                  var addnewsrows = function() {
                        var newstable = document.getElementById("newstable");
                        var newsrows = document.createElement("div");
                        var length = document.getElementsByName("newsrows").length;
                        newsrows.id = "newsrows_" + length;
                        newsrows.className = "newsrows1";
                        //newsrows.name = "newsrows";无法设置name
                        newsrows.setAttribute("name","newsrows");
                        newstable.appendChild(newsrows);
                  }
> - 复制节点cloneNode(bool)  当里面的布尔值为true的时候复制后代在内的所有，如果是false的话就仅复制自己；
                
                /* 通过复制的方式添加节点cloneNode()
                   * 当contentbox高度增加的时候添加节点
                   */
                  var addnewsrows = function() {
                        var newstable = document.getElementById("newstable");
                        var oldnewsrows = document.getElementById("newsrows_1");
                        var newsrows = oldnewsrows.cloneNode(true);
                        length = document.getElementsByName("newsrows").length;
                        lengths=length+1;
                        newsrows.id = "newsrows_" + lengths;
                        newstable.appendChild(newsrows);
                        var newsinterest=document.getElementsByName("newsinterest")
                        newsinterest[length].id="newsinterest_"+ lengths;
                        newsrows.addEventListener('mouseenter', newsinterest_mouseenter.bind(newsinterest[length]), false);
                        newsrows.addEventListener('mouseleave', newsinterest_mouseleave.bind(newsinterest[length]), false);
                  }        
> - 增加节点insertBefore(newNode,existNode) 在已存在的子元素的前面插入新的元素。
> - 删除节点removeChild(childrenObj) 作用在父元素上
        
                fatherObj.removeChild(childrenObj)
> - 替换节点replaceChild(newNode, oldNode)
        
                fatherObj.replaceChild(newNode, oldNode)
> - 文档节点documentFragment
>> - 作为其他节点的一个临时容器而存在； 
>> - var frag = document.createDocumentFragment();
>> - 它的parentNode总是为null
>> - 它的特殊之处在于：如果把它作为一个节点传递给appendChild(),insertBefore()或者replaceChild(),相当于把它里面的所有子节点插入到文档中，而非片段本身，此时文档片段被清空以便重用。另外，给文档片段添加子节点的时候，原来的子节点被清除。
>> - 其实就相当于剪切和粘贴的作用
>>>>>> ![图4-1 文档片段](https://github.com/hblvsjtu/JavaScript_Study/blob/master/picture/%E5%9B%BE4-1%20%E6%96%87%E6%A1%A3%E7%89%87%E6%AE%B5.png?raw=true)  
           
<h3 id='3.7'><a href="https://blog.csdn.net/qq_34986769/article/details/52160532">3.7 document.write()</a></h3> 
        
#### 1) 格式: 
>> - 在调用document.write，最好不要把document.open和document.close漏掉，尽管多数时候浏览器会帮忙完成这些操作。即，一个标准的document.write应该是这样的：

                document.open();
                document.write('anthing')
                document.close(); 
#### 2) 弊端 
>> - 从某个角度说，document.write的实际功能确实很强，能够直接修改文档流，但它有很多弊端：在非loading阶段调用document.write会清除已加载的页面；
>> - document.write不能够在XHTML中使用；
>> - 嵌入script中的document.write不能给任意节点添加子节点，因为它是随着DOM的构建执行的；
>> - 利用document.write写入HTML字符串流并不是一个好方法，它有违DOM操作的概念；
>> - 利用document.write添加script加载外部脚本时，浏览器的HTML解析会被script的加载所阻塞；

<h3 id='3.8'>3.8 文档和元素的几何形状和滚动</h3>                
        
#### 1) 文档坐标和视口坐标
> - 元素的坐标用像素作为单位来度量，向右表示X坐标增加，向下代表Y坐标增加
> - "视口"不包括浏览器的外壳（如菜单栏，工具栏等），而是实际显示文档内容的浏览器的一部分；
> - 如果文档要比视口要小，说明还没有出现滚动。其转换公式为：
                
                文档X坐标 = 视口X坐标 + 滚动偏移量X
                文档Y坐标 = 视口Y坐标 + 滚动动偏移量Y 
#### 2) 滚动偏移量
> - 提供滚动条的位置 除IE8及更早的版以外所有的浏览器，均可使用pageXOffest和pageYOffest属性获得，而所有的IE都可以使用scrollLeft和scrollTop属性获得滚动条的位置。不过比较奇怪的是，在怪异模式下，必须通过body元素来查询，而在普通模式下则是通过html元素获得；
        
                /* checkScrollOffset
                 * 获取窗口滚动条的偏移量
                 */
                var checkScrollOffset = function(gundong_X, gundong_Y, myWindow) {
                    
                    //使用指定接受参数的元素
                    var gundong_X = document.getElementById(gundong_X);
                    var gundong_Y = document.getElementById(gundong_Y);
    
                    //使用指定的窗口，如果不带参数则使用当前窗口
                    var w = myWindow || window;
                    var d = w.document;
    
                    //除IE8及之前的版本，其他所有的浏览器都能用
                    if(w.pageXOffset != null) {
                        gundong_X.innerHTML = "正常版本_" + w.pageXOffset;
                        gundong_Y.innerHTML = "正常版本_" + w.pageYOffset;
                    }
                    
                    //标准模式下的IE浏览器或其他所有的浏览器
                    
                    else if(document.compatMode == "CSS1Compat") {
                        gundong_X.innerHTML = "标准模式_" + d.documentElement.scrollLeft;
                        gundong_Y.innerHTML = "标准模式_" + d.documentElement.scrollTop;
                    }
    
                    //怪异模式下的IE浏览器或其他所有的浏览器
                    else {
                        gundong_X.innerHTML = "怪异模式_" + d.body.scrollLeft;
                        gundong_Y.innerHTML = "怪异模式_" + d.body.scrollTop;
                    }   
                }
    
                document.addEventListener("mousemove", function() {
                        checkScrollOffset("gundong_X", "gundong_Y");
                }, false);
#### 3) 视窗大小
> - 提供视窗的宽度和高度 除IE8及更早的版以外所有的浏览器，均可使用innerWidth和innerHeight属性获得，而所有的IE都可以使用clientWidth和clientHeight属性获得视窗的大小。不过比较奇怪的是，在怪异模式下，必须通过body元素来查询，而在普通模式下则是通过html元素获得；
        
                /* getViewportSize
                 * 获取视窗的宽度和高度
                 */
                var getViewportSize = function(shichuang_X, shichuang_Y, myWindow) {
    
                    var shichuang_X = document.getElementById(shichuang_X);
                    var shichuang_Y = document.getElementById(shichuang_Y);
    
                    //使用指定的窗口，如果不带参数则使用当前窗口
                    var w = myWindow || window;
                    var d = w.document;
    
                    //除IE8及之前的版本，其他所有的浏览器都能用
                    if(w.pageXOffset != null) {
                        shichuang_X.innerHTML = "正常版本_" + w.innerWidth;
                        shichuang_Y.innerHTML = "正常版本_" + w.innerHeight;
                    }
                    
                    //标准模式下的IE浏览器或其他所有的浏览器
                    
                    else if(document.compatMode == "CSS1Compat") {
                        shichuang_X.innerHTML = "标准模式_" + d.documentElement.clientWidth;
                        shichuang_Y.innerHTML = "标准模式_" + d.documentElement.clientHeight;
                    }
    
                    //怪异模式下的IE浏览器或其他所有的浏览器
                    else {
                        shichuang_X.innerHTML = "怪异模式_" + d.body.clientWidth;
                        shichuang_Y.innerHTML = "怪异模式_" + d.body.clientHeight;
                    }   
                }
    
                document.addEventListener("mousemove", function() {
                        getViewportSize("shichuang_X", "shichuang_Y");
                }, false);
#### 4) 查询元素的几何尺寸
> - IE5引入了getBoundingClinetRect()，返回一个有left，right，top和bottom属性的对象，left，top表示左上角的以视窗为参考系的X和Y坐标，right和bottom属性表示的是以视窗为参考系的右下角的X和Y坐标。这个坐标以元素的边框为边界。后来被标准收入并广泛传播到其他浏览器。
        
                /* getElementSize
                 * 获取元素的宽度和长度
                 */
                var getElementSize = function(myElement) {
                        var myElement = document.getElementById(myElement);
                        var box = myElement.getBoundingClientRect();
                        console.log("box的左上角X坐标："+ box.left +"px;");
                        console.log("box的左上角Y坐标："+ box.top +"px;");
                        console.log("box的右下角X坐标："+ box.right +"px;");
                        console.log("box的右下角Y坐标："+ box.bottom +"px;");
                }
            
                var myElement = document.getElementById("position");
                myElement.addEventListener("mousemove", function() {
                        getElementSize("position");
                }, false);
> - 如果想要查询行内元素的具体尺寸，需要单独采用getClinetRect(),返回的内容跟getBoundingClinetRect()类似，是一个类数组的对象。
> - 关于实时性的问题，大多数DOM方法都是实时更新的，但是getBoundingClinetRect()和getClinetRect()却不是，他只是一个瞬时的快照
#### 5) 判断某元素在某点
> - elementFromPoint(),参数是X坐标和Y坐标，返回在视窗范围内某坐标上的一个元素，如果某点在视窗之外，则返回null。由于鼠标的事件对象的target属性已经包含了这些信息，所以这个功能显得有些鸡肋。
#### 6) 鼠标事件
>>>>>> ![图2-2 鼠标事件.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE2-2%20%E9%BC%A0%E6%A0%87%E4%BA%8B%E4%BB%B6.png?raw=true)
#### 7) 滚动
> - scrollTo(X，Y)或着scroll(X，Y) 接受两个参数，分别是相对于视窗的X坐标和Y坐标，那个点将会出现在视窗的左上角，属于window的属性；
> - scrollBy(X，Y)，接受两个参数，分别是相对于视窗的X坐标和Y坐标，那个点将会出现在视窗的左上角，属于window的属性；
                
                // 注意它一旦开始就没办法停止^-^
                setInterval(function() {scrollBy(0,-10)}, 1000); 
> - scrollIntoView()的行为是尽量将所选择的元素放在视窗中，默认把元素的上边缘尽量靠经视窗的上边缘，如果传递false作为参数，则把元素的下边缘尽量靠经视窗的下边缘，类似于a元素的锚点功能；
#### 8) 滚动关于元素尺寸，位置和溢出
> - offsetLeft和offSetHeigt是以文档坐标为参考的
>>>>>> ![图2-3 关于元素尺寸，位置和溢出](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE2-3%20%E5%85%B3%E4%BA%8E%E5%85%83%E7%B4%A0%E5%B0%BA%E5%AF%B8%EF%BC%8C%E4%BD%8D%E7%BD%AE%E5%92%8C%E6%BA%A2%E5%87%BA.png?raw=true)
           
                /* 判断元素是否溢出
                 * 先利用clientHeight获取元素高度，在利用scrollHeight获取内容高度
                 * 然后比较这两个高度，如果scrollHeight>clientHeight,则溢出
                 */ 
                 var isOverflow = function(ele) {
                    var element = document.getElementById(ele);
                    var scrollHeight = element.scrollHeight;
                    var clientHeight = element.clientHeight;
                    if(scrollHeight > clientHeight) {
                        console.log(ele + "溢出了");
                    }else {
                        console.log(ele + "没有溢出");
                    }
                 }
                 document.addEventListener("mousemove", function() {
                        isOverflow("contentbox");
                 }, false); 
------ 
            
<h2 id='4'> 四、事件处理 </h2>        
<h3 id='4.1'>4.1 简介</h3>    
        
#### 1) 简介
> -  异步事件驱动编程模型，广泛应用于图形界面；
> -  事件类型
> -  事件目标
> -  事件处理程序或事件监听程序
> -  事件对象，至少包含事件类型和事件目标等信息
> -  事件传播，比如冒泡；
> -  [1-1 事件处理概念.png](https://blog.csdn.net/wuqinfei_cs/article/details/48413809) 
>>>>>> ![1-1 事件处理概念.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/1-1%20%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E6%A6%82%E5%BF%B5.png?raw=true)        
        
<h3 id='4.2'>4.2 事件类型 </h3>    

#### 1) 传统事件类型   
> - 表单事件
> - window事件
>> - 比如著名的onload()，仅在文档及图片全部加载完毕时触发。 
>> - DomContentLoaded()，当文档加载解析完毕且所有延迟脚本都执行完毕时会触发，此时图片和异步（async）脚本可能还在加载
>> - document.readyState属性随着文档加载过程而变，每次改变都伴随着document上的readystatechange事件
>> - whenReady函数
> - 鼠标事件
> - 键盘事件
#### 2) DOM事件
#### 3) HTML5事件
> - audio和video
> - drag
> - 历史管理机制
> - HTML表单
> - 离线web应用
#### 4) 注册事件处理程序
> - 设置HTML标签属性为事件处理程序（不推荐）
> - addEventListener()和removeEventListener()
> - attachEvent()和detachEvent()，IE不支持事件捕获，但允许同一事件处理程序注册多次，且事件触发时，程序执行次数和注册次数一样
    
<h3 id='4.3'>4.3 注册事件处理程序 </h3>    
        
#### 1) 两种方法 
> - 直接给事件目标对象或者元素设置属性，这种方法出现在Web初期比较多；利用JS将事件处理程序传递给对象或者元素；
> - (1) 设置JS对象的属性添加事件处理程序
>> - 由于属性名区分大小写，所以约定所有都是小写，on+事件名，这种方法适用于所有浏览器的所有常用事件类型，但是这种方法也有一个缺陷是，每个属性最多添加一个事件处理函数，意味着后来的事件处理函数会覆盖前面的事件处理函数。如： 
               
               window.onload = function() {
                    var elt = document.getElementById("myform");
                    elt.onsubmit = function() { 
                        return validate(this);
                    }
                } 
> - (2) 设置HTML标签属性为事件处理程序 
>> - 具体就是用于设置的文档元素时间处理程序属性property换成对应的HTML标签的属性attribute。如果这样做，属性值应该是JS代码的字符串，而非完整的函数声明，也就意味着HTML时间处理程序的程序代码不应该用大括号包围而且使用function关键字作为前缀。如：<button onclick="alert('Hello');" >点击这里</button>                 
        
                <button onclick="alert('Hello');" >点击这里</button>
                       
>> - 但是实际上浏览器会把该代码转为类似如下的完整代码：

                function() {
                    with(document);
                        with(this.form || {}) {
                            with(this) {
                                /* 这里是程序代码 */
                            }
                        }       
                }       
>> - 由于客户端编程的风格偏向于把内容和行为分离，所以并不支持用这种方式；
>> - 还有一些是直接作用在浏览器而非某个单独的元素，其完整的HTML5事件处理程序列表如下：
>>>>>> ![1-2 完整的HTML5事件处理程序列表.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/1-2%20%E5%AE%8C%E6%95%B4%E7%9A%84HTML5%E4%BA%8B%E4%BB%B6%E5%A4%84%E7%90%86%E7%A8%8B%E5%BA%8F%E5%88%97%E8%A1%A8.png?raw=true)   
    
> - (3) addEventListener(type, func, bool)与removeEventListener(type, func, bool) 
>> - 适用范围：除IE8及之前版本外的所有浏览器
>> - 三个参数 type是事件类型的字符串，不带“on”前缀；func是非立即执行事件处理程序，不带参数，如果强行需要带参数的话，可以在外面嵌套一个function(){//执行代码},然后参数直接写进执行代码中； bool值是true的话，那么函数将会注册为捕获事件处理程序，并在事件不同的调度阶段调用。不过一般我们会默认用false。[布尔值参数是true，表示在捕获阶段调用事件处理程序；就是最不具体的节点先接收事件，最具体的节点最后接收事件;如果是false，在冒泡阶段调用事件处理程序;则是先寻找指定的位置，由最具体的元素接收，然后逐级向上传播至最不具体的元素的节点（文档）。由图可知捕获过程要先于冒泡过程即，true的触发顺序在false前面](https://blog.csdn.net/qq_29606781/article/details/67650869)。
>>>>>> ![DOM事件流如图（剪自javascript高级程序设计）](http://images.cnitblog.com/i/187577/201407/110857551929664.png)
>> - 可以同时为事件对象注册相同类型的多个不同事件处理程序，但是如果连事件处理程序都相同的话那只能执行一个。
>> - 与之相对的还有removeEventListener(type, func, bool)，用于移除相关的监听器，由于需要捕获相关的事件，可以灵活使用bool=true，需要注意的是，removeEventListener函数与对应的addEventListener函数的第二个参数必须使用相同的引用，意味着不能直接把函数的定义全都写进去，必须在外面写好引用再传递过去。如：
        
        //当mousemove事件到来后，可以注销相关的时间处理程序
        var length = document.getElementsByName("newsrows").length;
                for(i=1; i<length+1; i++) {
                    (function() {
                        var newsrows=document.getElementById("newsrows_"+i);
                        var newsinterest=document.getElementById("newsinterest_"+i);
                        console.log(newsrows);
                        var newsinterest_mouseenter=function() {
                            newsinterest.style.visibility='visible';
                        };
                        var newsinterest_mouseleave=function() {
                            newsinterest.style.visibility="hidden";
                        };
                        newsrows.addEventListener('mouseenter', newsinterest_mouseenter, false);
                        newsrows.addEventListener('mouseleave', newsinterest_mouseleave, false);
                        newsrows.removeEventListener('mouseleave', newsinterest_mouseleave, false);
                    })();
                }
        
> - (4) attachEvent(type, func)与detachEvent(type, func) 
>> - 适用范围：IE5~IE8
>> - 与addEventListener和removeEventListener不同的地方有三个：A：attachEvent(type, func)与detachEvent(type, func)不支持事件捕获，所以只有两个参数；B：相同事件目标相同事件类型可以注册多个相同或者不相同的事件处理程序，注册的次数和函数的个数相同；attachEvent(type, func)与detachEvent(type, func)的事件类型需要有前缀“on”;
        
<h3 id='4.4'>4.4 循环绑定事件</h3>        
        
#### 1) [误区](https://www.cnblogs.com/yangjiewu/p/4753202.html)
> - 这段代码如果不仔细看的话会误以为三个按钮点击结果分别为0，1，2。但是运行结果却是3，3，3。我们来分析一下代码执行过程：前三遍循环分别给按钮0，1，2绑定了alert(i)的事件，第四遍循环开始时i=3，不符合i<=2的条件，因此终止循环。这里要注意的是，前三遍循环绑定的是alert(i)事件，而不是alert(0)，alert(1)，alert(2)，因为在绑定的过程中on的事件处理函数里的代码并没有运行，因此在触发click事件之前并不知道i等于几，代码此时只认为i是一个全局变量（实际上i的作用域为最外层的function）。上面分析了，当循环结束时i等于3，因此3个按钮点击均为alert(3)。
        
                <button id="0">0</button>
                <button id="1">1</button>
                <button id="2">2</button>
                <script> 
                $(function(){
                    for (var i=0; i<=2; i++) {
                        $("#" + i).on("click", function() {
                            alert(i);
                        });
                    };
                })
                </script>
#### 2) [原生的解决方案](https://www.cnblogs.com/yangjiewu/p/4753202.html)
> - 在on函数的外层写一个立即执行的函数，其目的是生成作用域，循环三遍即生成三个作用域，i的值由最下面的参数传入，三个作用域互不影响，因此也可以实现循环绑定的效果   
        
                for (var i=0; i<=2; i++) {
                    (function(i) {
                        $("#" + i).on("click", function(){
                            alert(i);
                        });
                    })(i);
                };
                
            或者：
                var length = document.getElementsByName("newsrows").length;
                for(i=1; i<length+1; i++) {
                    (function() {
                        var newsrows=document.getElementById("newsrows_"+i);
                        var newsinterest=document.getElementById("newsinterest_"+i);
                        console.log(newsrows);
                        var newsinterest_mouseenter=function() {
                            newsinterest.style.visibility='visible';
                        };
                        var newsinterest_mouseleave=function() {
                            newsinterest.style.visibility="hidden";
                        };
                        newsrows.addEventListener('mouseenter', newsinterest_mouseenter, false);
                        newsrows.addEventListener('mouseleave', newsinterest_mouseleave, false);
                    })();
                }
        
            或者：
                var newsrows=document.getElementsByName("newsrows");
                var newsinterest=document.getElementsByName("newsinterest");
                for(i=0; i<3; i++) {
                    (function(newsrows,newsinterest) {
                        var newsinterest_mouseenter=function() {
                            newsinterest.style.visibility='visible';
                        };
                        var newsinterest_mouseleave=function() {
                            newsinterest.style.visibility="hidden";
                        };
                        newsrows.addEventListener('mouseenter', newsinterest_mouseenter, false);
                        newsrows.addEventListener('mouseleave', newsinterest_mouseleave, false);
                    })(newsrows[i],newsinterest[i]);
                }
    
            或者：
                var newsrows=document.getElementsByName("newsrows");
                var newsinterest=document.getElementsByName("newsinterest");
                var newsinterest_mouseenter=function(e) {
                    e.style.visibility='visible';
                };
                var newsinterest_mouseleave=function(e) {
                    e.style.visibility="hidden";
                };
                for(i=0; i<3; i++) {
                    (function(newsrows,newsinterest) {
                        newsrows.addEventListener('mouseenter', function() {
                                                                    newsinterest_mouseenter(newsinterest);
                                                                }, false);
                        newsrows.addEventListener('mouseleave', function() {
                                                                    newsinterest_mouseleave(newsinterest);
                                                                }, false);
                    })(newsrows[i],newsinterest[i]);
                }
            或者：
                var newsrows=document.getElementsByName("newsrows");
                var newsinterest=document.getElementsByName("newsinterest");
                var newsinterest_mouseenter=function() {
                    this.style.visibility='visible';
                };
                var newsinterest_mouseleave=function() {
                    this.style.visibility="hidden";
                };
                for(i=0; i<3; i++) {
                    newsrows[i].addEventListener('mouseenter', newsinterest_mouseenter.bind(newsinterest[i]), false);
                    newsrows[i].addEventListener('mouseleave', newsinterest_mouseleave.bind(newsinterest[i]), false);
                }
        
<h3 id='4.5'>4.5 事件处理程序的调用</h3>                
        
#### 1) 事件对象
> - 事件对象用event表示，在IE8之前，当调用属性注册事件处理程序的时候，如果为传递event，则会通过全局对象window.event来获取事件对象：
        
                function() {
                    event = event || window.event;
                    //事件处理程序或事件监听程序代码；
                }
#### 2) 事件处理程序的运行环境
> - 运行环境一般就是事件目标，直白一点说即this关键字指的就是事件目标；
> - 但是在IE8及以前的attachEvent与detachEvent，this关键字指的却是全局Window对象，可以使用如下代码解决这个问题：
        
                function addEvent(target, type, handler) {
                        if(target.addEventListener()) {
                            target.addEventListener(type, handler, false);
                        }else {
                            target.attachEvent("on"+type,
                                    function(event) {
                                        return handler.call(target,event);
                                    }); //注意：该函数不能通过detachEvent函数进行解除，因为该函数的引用并没有保留下来；
                        }
                }

#### 3) 事件处理程序的作用域
> - 如果忘了JS的作用域可以[点击这里](https://www.cnblogs.com/skylar/p/3986087.html), 或者[这里](https://blog.csdn.net/qq_23980427/article/details/54645701),又或者是大名鼎鼎的[阮一峰同学的个人网站](http://es6.ruanyifeng.com/#docs/let)
> - 关于javascript中call()、apply()、bind()的用法理解可以[看这里](https://www.cnblogs.com/Shd-Study/archive/2017/03/16/6560808.html)
> - 像所有的JS函数一样，事件处理程序的在其定义时的作用域中执行，而非调用时的作用域
> - **扩展作用域**   HTML属性注册函数，实际上，这样扩展作用域的方式，无非就是让事件处理程序无需引用表单元素就能访问其他表单字段。
>>>>>> ![HTML属性注册函数作用域简要说明](https://pic2.zhimg.com/688ced70669d07c5659b8304dd75eed4_r.jpg)
    
#### 4) 调用顺序
> - 设置HTML标签属性为事件处理程序优先；
> - 使用addEventLisener()注册事件处理程序按照它们的注册顺序来调用；
> - 使用attachEvent()注册事件处理程序可能按照任何顺序调用；
        
#### 5) 事件传播的三个阶段
> - 第一阶段：事件捕获；
> - 第二阶段：目标对象本身的事件处理程序调用；
> - 第三阶段：事件冒泡；
> - [事件委托](https://www.cnblogs.com/liugang-vip/p/5616484.html)

#### 6) [事件取消](https://blog.csdn.net/wxl1555/article/details/53128966)
> - 取消浏览器的默认操作。event.preventDefault()方法。这是阻止默认事件的方法，调用此方法是，连接不会被打开，但是会发生冒泡，冒泡会传递到上一层的父元素。
        
                $(".box1 a").click(function(event){           
                    //阻止默认事件  
                    event.preventDefault();//页面不会跳转，但是会打印出1，  
                })；  
                              
                $(".box1").click(function(){  
                console.log("1")；                 
                });         

> - 取消事件传播，如果在同一对象上定义了其他处理程序，剩下的处理程序将依旧被调用，但是调用event.stopPropagation后其他对象的事件处理程序将不会被调用，另外该方法可以在事件传播的各个阶段被调用；
                
                $(".box1").click(function(){  
                    console.log("1")//不阻止事件冒泡会打印1，页面跳转;               
                });
    
                //阻止冒泡  
                $(".box1 a").click(function(event){  
                    event.stopPropagation();//不会打印1，但是页面会跳转；              
                });
    
            或者
                //event是事件对象
                box.onmouseover = function (event) {
                    // 阻止冒泡
                    event = event || window.event;
                    if(event && event.stopPropagation){
                        event.stopPropagation();    //IE不支持event.stopPropagation
                    }else{
                        event.cancelBubble = true;  //IE支持event.cancelBubble
                    }
                }
> - return false  这个方法比较暴力，他会同事阻止事件冒泡也会阻止默认事件；写上此代码，连接不会被打开，事件也不会传递到上一层的父元素；可以理解为return false就等于同时调用了event.stopPropagation()和event.preventDefault()
    
<h3 id='4.6'>4.6 文档加载事件</h3>                
        
#### 1) 执行顺序
> - 文档加载解析(同步下载JS脚本文件)完毕  -->   
> - 延迟（deferred）脚本执行完毕  -->   
> - document对象触发DOMContentLoaded事件，标志着程序执行从同步脚本执行阶段切换到异步事件驱动阶段，但是需要注意的是异步脚本没有执行完成  -->  
> - 文档完全解析完成，但浏览器还在等待相关资源的载入，如图片，还有异步脚本还在执行  --> 
> - 当所有资源载入和所有异步脚本执行完毕后，complete，Web浏览器触发Windows对象上的load事件  -->   
> - 调用异步事件，以异步相应客户的输入
>>>>>> ![图2-1 事件执行顺序.png](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE2-1%20%E4%BA%8B%E4%BB%B6%E6%89%A7%E8%A1%8C%E9%A1%BA%E5%BA%8F.png?raw=true)
#### 2) 测试代码：
> - index.js代码：
        
                //index.js代码
                console.log("加载index.js完成");
> - HTML:代码：
                
                //HTML:代码
                <!DOCTYPE html>
                <html>
                <head>
                    <meta charset="utf-8">
                    <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1">
                    <title>文档加载事件顺序</title>
                    <meta name="description" content=""/>
                    <meta name="keywords" content=""/>
                    <link href="./test.css" rel="stylesheet">
                    <script>
                            var i=0;
                            if(document.readyState === "loading") {
                                console.log("目前document.readyState = loading");
                            }
    
                            document.onreadystatechange = function () {
                                console.log("第"+(++i)+"次状态改变；");
                                console.log("目前document.readyState = "+document.readyState);   
                            }
    
                            document.addEventListener("DOMContentLoaded", function (event) {
                                console.log("初始DOM，加载并解析完成，触发DOMContentLoaded事件");
                            });
    
                            window.addEventListener("load", function (event) {
                                console.log("window 所有资源加载完成，触发Load事件");
                            });
    
    
                            window.addEventListener("beforeunload", function (event) {
                                console.log('即将关闭')
                                event.returnValue = "\o/";
                            });
    
                            window.addEventListener('unload', function (event) {
                                console.log('即将关闭1');
                            });
                        </script>    
                    </head>
        
                    <body>
                        <div id="root">dom事件</div>
                        <script src="./index.js"></script>
                    </body>
                </html>
> - 测试结果：
                
                //测试结果：
                Failed to load resource: net::ERR_FILE_NOT_FOUND

                目前document.readyState = loading

                index.js:8 加载index.js完成

                第1次状态改变；

                目前document.readyState = interactive

                初始DOM，加载并解析完成，触发DOMContentLoaded事件

                第2次状态改变；

                目前document.readyState = complete

                window 所有资源加载完成，触发Load事件

                即将关闭

<h3 id='4.7'>4.7 几种页面跳转的方法 具体请看<a href="https://blog.csdn.net/cordova/article/details/50853451">Mr_厚厚的博客</a></h3>                
        
#### 1) 定时跳转或者原地刷新
> - 对于刷新当前页面js控制为：
    
                window.location.reload();//刷新当前页面，重新向服务器请求数据
> - head标签内部的meta标签方式，定时刷新当前界面或刷新到另一个页面：
                
                // 3秒后跳转到another.html页面
                <meta charset="utf-8" http-equiv="refresh" content="3;url=another.html">    
#### 2) js手动替换跳转
> - 优点：灵活，可以结合更多的其他功能
> - 缺点：受到不同浏览器的影响
> - 上面的方法跳转会保留历史页面记录，通过返回键可以返回上一个界面，如果不想返回，直接替换页面的函数：
                
                //刷新当前页面，重新向服务器请求数据  
                window.location.replace("hello.html");

                或者
                window.location.href="hello.html";
#### 3) js手动新建跳转
> -    window.open(url);
    
                window.open("hello.html");
#### 4) 历史记录跳转
> - window.history.go():
    
                window.history.go(-1); // 返回上一页  
                  
                window.history.go(-2); // 返回上两页  
                  
                window.history.go("hello.html");// 跳转到hello.html  
> - window.history.back()
    
                window.history.back();

                等同于：window.history.go(-1);//返回上一页

                window.history.forward(); //返回下一页

        

------ 
            
<h2 id='5'> 五、脚本化CSS </h2>        
<h3 id='5.1'>5.1 脚本化内联样式</h3>    
        
#### 1) CSSStyleDeclaration对象
> - style是元素的属性，而CSSStyleDeclaration是style的属性，如：
        
                e.style.fontSize = "24pt";
> - CSSStyleDeclaration对象的值都是字符串  
> - 复合属性
        
                 e.style.border = topMargin + "px " + bottomMargin + "px "
                        + leftMargin + "px " + rightMargin + "px"; 
> - 内联样式的优先级一般都会比样式表的要高；
#### 2) cssText 具体的可以看[这里](https://www.cnblogs.com/majingyi/p/6840818.html)
> - cssText 的本质就是设置 HTML 元素的 style 属性值，
        
                obj.style.cssText=”样式”;
                element.style.cssText=”width:20px;height:20px;border:solid 1px red;”;  
> - 但是，这样会有一个问题，会把原有的cssText清掉，比如原来的style中有’display:none;’，那么执行完上面的JS后，display就被删掉了。为了解决这个问题，可以采用cssText累加的方法：
        
                 Element.style.cssText += ‘width:100px;height:100px;top:100px;left:100px;’
> - 因此，上面cssText累加的方法在IE中是无效的。最后，可以在前面添加一个分号来解决这个问题：
        
                Element.style.cssText += ‘;width:100px;height:100px;top:100px;left:100px;’
> - 再进一步，如果前面有样式表文件写着 div { text-decoration:underline; }，这个会被覆盖吗？不会！因为它不是直接作用于 HTML 元素的 style 属性。
> - 内联样式的setter和getter
        
                //setter
                e.setAttribute("style", s);
                e.style.cssText = s;

                //getter
                s = e.getAttribute("style");
                s = e.style.cssText;

#### 3) window.getComputedStyle(element, 伪元素)
> - 这个属性是属于浏览器窗口的，第一个参数是你想要计算的元素，第二个参数表示第一个参数的伪元素，但也可以是null或者是空字符串，最后返回一个CSSStyleDeclaration对象
> - 所以可以利用返回的CSSStyleDeclaration对象来读取某个具体的属性，如font-size；
> - 计算样式的CSSStyleDeclaration对象和内联元素的CSSStyleDeclaration对象是有区别的
>> - 计算样式的属性是只读的
>> - 计算样式的值是绝对值，这意味着单位是px或者“rgb(#, #, #)” 或者“rgba(#, #, #, #)”
>> - 不计算复合属性，也就是说不能直接返回margin属性，只能基于基本属性，如：margin-left;
>> - 计算样式的cssText属性没有定义；
>> - 在IE8及之前没有实现           
#### 4) currentStyle 具体的可以看[张鑫旭老师的博客](http://www.zhangxinxu.com/wordpress/2012/05/getcomputedstyle-js-getpropertyvalue-currentstyle/)
> - currentStyle是IE浏览器自娱自乐的一个属性，其与element.style可以说是近亲，至少在使用形式上类似，element.currentStyle，差别在于element.currentStyle返回的是元素当前应用的最终CSS属性值（包括外链CSS文件，页面中嵌入的style元素的属性等）。
> - 因此，从作用上讲，getComputedStyle方法与currentStyle属性走的很近，形式上则style与currentStyle走的近。不过，currentStyle属性貌似不支持伪类样式获取，这是与getComputedStyle方法的差异，也是jQuery css()方法无法体现的一点。  
#### 5) getPropertyValue方法 具体的可以看[张鑫旭老师的博客](http://www.zhangxinxu.com/wordpress/2012/05/getcomputedstyle-js-getpropertyvalue-currentstyle/)
> - getPropertyValue方法可以获取CSS样式申明对象上的属性值（直接属性名称），例如：
        
                window.getComputedStyle(element, null).getPropertyValue("float");
> - 如果我们不使用getPropertyValue方法，直接使用键值访问，其实也是可以的。但是，比如这里的的float，如果使用键值访问，则不能直接使用getComputedStyle(element, null).float，而应该是cssFloat与styleFloat，自然需要浏览器判断了，比较折腾！
> - 使用getPropertyValue方法不必可以驼峰书写形式（不支持驼峰写法），例如：style.getPropertyValue("border-top-left-radius");
        
<h3 id='5.2'>5.2 脚本化CSS类</h3>    
        
#### 1) className
> - 直接方法
        
                e.className = "某类名1 某类名2"；
> - 直接方法有个缺点，它会覆盖原有的方法
#### 2) classList 具体的可以看[张鑫旭老师的博客](http://www.zhangxinxu.com/wordpress/2013/07/domtokenlist-html5-dom-classlist-%E7%B1%BB%E5%90%8D/)
> - HTML5中为每个元素都定义了classList，该属性值是DOMTokenList对象————一个只读的类数组对象
> - classList的返回值显示，其本质上是DOMTokenList – DOM标记列表.
> - DOMTokenList这种类型表示一组空间分隔的标记。通常由HTMLElement.classList, HTMLLinkElement.relList, HTMLAnchorElement.relList或HTMLAreaElement.relList返回。从0开始的类JavaScript数组索引。DOMTokenList始终是区分大小写的。
> - 在FireFox以及Chrome下，我们执行typeof DOMTokenList的结果是："function"; 但是在IE10下，却是："object".IE10 DOMTokenList对象类型同时虽然typeof结果为"function"，但是执行DOMTokenList()会报”Illegal constructor”错误；IE10执行DOMTokenList()也会报错，错误是”缺少函数”。因此，试图通过typeof obj == "function"来判断obj就是个函数的做法是不完全正确的。
                
                //在控制台中输入
                document.getElementById('newsrows_1').classList；
                document.getElementById('newsrows_1').classList.item(0);

                //返回结果
                DOMTokenList ["newsrows2", value: "newsrows2"]
                "newsrows2"

                //DOMTokenList被暴露的属性
                __proto__: DOMTokenList     
                0: "newsrows2"
                length: 1
                value: "newsrows2"
                add:ƒ add()
                contains: ƒ contains()
                entries: ƒ entries()
                forEach: ƒ forEach()
                item: ƒ item()
                keys: ƒ keys()
                length: (...)
                remove: ƒ remove()
                replace: ƒ replace()
                supports: ƒ supports()
                toString: ƒ toString()
                toggle: ƒ toggle()
                value: (...)
                values: ƒ values()
                constructor: ƒ DOMTokenList()
                Symbol(Symbol.iterator): ƒ values()
                Symbol(Symbol.toStringTag): "DOMTokenList"
                get length: ƒ ()
                get value: ƒ ()
                set value: ƒ ()
                __proto__: Object

> - 拥有add()和remove()方法
        
                document.body.classList.add("c");
                document.body.classList.length    // 3
> - classList的局限
>> - classList除了上面提到的不能级联这个无关痛痒的局限外，还有个比较头疼的局限，就是不能一次add或remove或toggle多个类名。//zxx: 级联指的是$().a().b().c()这种可以连在一起调用方法的写法。例如：
        
                document.body.classList.add("c d");    // Error: String contains an invalid character
                document.body.classList.add("c\x20d");   // Error: String contains an invalid character
                document.body.classList.remove("c d");    // Error: String contains an invalid character
>> - 我们要想多类名处理，需要一个一个来，例如：
        
                var clList = document.body.classList;
                clList.add("d");
                clList.add("e");
        
<h3 id='5.3'>5.3 脚本化样式表 具体看<a href="https://www.cnblogs.com/limingxi/p/4526518.html">李明夕同学的博客</a></h3>    
        
#### 1) document.styleSheets
> - 它是一个只读的类数组对象——CSSStyleSheet，表示与文档关联在一起的样式表，可以定义或者引用link元素或者style元素的title属性值       
#### 2) 开启和关闭样式表
            
                //关闭样式表
                document.styleSheets[0].disabled = true;

                //查询样式表
                document.styleSheets[0].href
                "http://localhost:8080/CompatTest/BaiduHomePage.css"
#### 3) 查询
> - 数组的元素是CSSStyleSheet对象，CSSStyleSheet对象有一个cssRule[]数组，包含如@import和@page等指令，在IE中使用rules[]代替cssRule[]，但是区别在于IE的rules[]只包含样式表中实际存在样式规则；
                
                document.styleSheets[0].cssRules[0]

    //结果
    CSSStyleRule {selectorText: "body", style: CSSStyleDeclaration, styleMap: StylePropertyMap, type: 1, cssText: "body { background: pink; }", …}
    cssText: "body { background: pink; }"
    parentRule: null
    parentStyleSheet: CSSStyleSheet {disable: true, ownerRule: null, cssRules: CSSRuleList, rules: CSSRuleList, type: "text/css", …}
    selectorText: "body"
    style: CSSStyleDeclaration {0: "background-image", 1: "background-position-x", 2: "background-position-y", 3: "background-size", 4: "background-repeat-x", 5: "background-repeat-y", 6: "background-attachment", 7: "background-origin", 8: "background-clip", 9: "background-color", alignContent: "", alignItems: "", alignSelf: "", alignmentBaseline: "", all: "", …}
    styleMap: StylePropertyMap {size: 10}
    type: 1
    __proto__: CSSStyleRule
> - 更加具体的查询相关属性
        
                document.styleSheets[0].cssRules[0].cssText;

    //结果
    "body { background: pink; }"

                document.styleSheets[0].cssRules[0].style.cssText;

    //结果
    background: pink;
> - 遍历样式表
                
                var ss = document.styleSheets[0];
                var rules = ss.cssRules?ss.cssRules:ss.rules;
                for(var i = 0; i < rules.length; i++) {
                    if(!rules[i].selectorText) {
                        continue;
                    } 
                    var selector = rules[i].selectorText; 
                    var ruleText = rules[i].style.cssText;
                    console.log(selector+": {" + ruleText + "}")};
[遍历样式表结果](#10.1)
#### 4) 获取样式表
> - 我们可以选择向页面内的某条stylesheet中添加样式。可以给link标签或者style标签添加ID，通过引用节点的sheet属性来获取CSSStyleSheet对象。页面中的stylesheets可以使用document.styleSheets来获取
#### 5) 添加样式表
> - 有些情况下，可能新建一个style节点来承装新添加的style rule。方法很简单：
    
                var addStyles = (function(styles) {
                    
                    var styleSheet, styleElt;
                    if(document.createStyleSheet) {
                        var styleSheet = document.createStyleSheet();
                    }else{

                        // Create the <style> tag
                        styleElt = document.createElement("style");
                        styleElt.appendChild(document.createTextNode(""));
                        document.head.appendChild(styleElt);

                        //新的样式表应该是最后一个
                        styleSheet = document.styleSheets[document.styleSheets.length-1];
                    }
    
                        //向样式表插入样式
                        if(typeof styles === "string") {
                            if(styleElt) {
                                styleElt.innerHTML = styles;
                            }else {
                                styleSheet.cssText = styles; //IE API
                            }
                        }else {

                            //强制使用insertRule或者addRule插入
                        }
                })("body {background: pink;}");  
#### 6) 插入样式表
> - **insertRule(styles,[index])** Stylesheets对象提供了insertRule（译者注：IE8及以下不兼容，具体参考链接http://www.quirksmode.org/dom/w3c_css.html ）
> - **方法** insertRule函数要求传入css样式风格的str作为参数。
> - **具体调用方法**：
        
               document.styleSheets[0].insertRule("body {background:pink;}", 1);
                //（译者注：传入的样式str的格式要求很多。就我目前发现的：
                // 1.{}两个花括号和前后最好都有一个空格 
                // 2.如果是webkit内核，函数在解析带有-moz-前缀的样式规则时会抛err）

                //结果
                body {
                    background: yellow;
                }
> - 这种方法看上去有点丑，但是确实有用。第二个参数Index，表示我们将在样式内部的哪一条插入新样式css rule，这就可以帮助我们实现原有样式的覆盖。默认index取值是-1(译者注：但是输入-1在chrome 41下抛了err，提示参数不能小于0，这里值得在研究一下)，表示默认在样式最后追加。如果想强制覆盖，可以使用！important，来避免插入次序引起其他问题。
> - **非标准函数  addRule(selector,styles,index)**  CSSStyleSheet对象有一个非标准函数addRule，和insertRule相比，它更像js api的调用风格，无需自己注意插入的样式字符串的格式。addRule方法接受三个参数，分别是选择器selector，样式字符串"color:red;font-size:12px",和插入次序index。
                
                document.styleSheets[0].addRule("body", "background: white;", 4);
                //方法有返回值，为-1。但是没有什么具体含义。
                //这种方式可以快速高效的改变页面上节点的已有样式。

                //结果
                body {
                    background: white;
                }
> - **应用样式** 因为上面提到两个函数都不是常见api函数，所以需要做浏览器兼容性处理。这种方法可以应用于所有高级的浏览器，如果还是有担心的话，可以在调用时使用try-catch结构
        
                function addCSSRule(sheet, selector, rules, index) {
                    if("insertRule" in sheet) {
                        sheet.insertRule(selector + "{" + rules + "}", index);
                    }
                    else if("addRule" in sheet) {
                        sheet.addRule(selector, rules, index);
                    }
                }

                // Use it!
                addCSSRule(document.styleSheets[0], "header", "float: left");
#### 7) 删除样式表
> - 直接删除样式表中一整条规则，包括里面的各个属性　　
            
                document.styleSheets[索引].deleteRule(索引);
                或者
                //仅对IE有效
                document.styleSheets[索引].removeRule(索引);

        
------      
         
        
<h2 id='6'> 六、HTTP脚本化 </h2>
<h3 id='6.1'>6.1 Ajax和Comet</h3>  

#### 1) Ajax 
> - Ajax Asynchronous JavaScript and XML，是一种使用脚本操纵HTTP的Web应用架构
> - 主要特点是使用脚本操纵HTTP和Web服务器进行数据Ajax Asynchronous JavaScript and XML，交换，不会导致页面重载。
> - 方向是从client指向server；
> - 异步
#### 2) Comet 
> - 也是一种使用脚本操纵HTTP的Web应用架构
> - 方向跟Ajax相反，server指向client
> - 在Comet中，Web服务器发起通信并异步发送消息到客户端。如果Web应用需要响应服务端发送的消息，则会利用Ajax技术发送或者请求数据
> - 服务器保持打开直到它需要推送一条消息，服务器每发送完一条消息就关闭连接，这样可以确保客户端正确接收到消息，处理该消息之后，客户端马上为后续的消息推送建立一个新的连接。
> - 异步
#### 3) 实现方式
> - img标签的src属性，通过URL用GET的方式传递消息给server，server必须返回一个图片作为请求结果，而且这个图片必须不可见，因为我只需要把信息从client指向server，不需要返回的消息，所以这个图片一般是一个1 X 1像素的透明图片。这种类型的图片又叫做网页信标(Web bug)，通常用于统计点击次数或者网站流量分析。但是它也有自己的缺陷，就是没办法返回有用的响应信息；
> - iframe元素更为强大，利用src属性设置URL，可以使用server返回的文档并从中读取有用的信息。一般把iframe元素设置为不可见即可，但是它也有一个限制：受同源策略的限制；
> - script元素，利用src属性设置URL并发起HTTP GET请求，由于其有规避同源策略的能力，且不受同源策略的限制
        
<h3 id='6.2'>6.2 XMLHttpRequest</h3>         
        
#### 1) XMLHttpRequest类
> - 浏览器的XMLHttpRequest类定义了它们的HTTP API。这个类的每个实例都表示一个独立的请求/响应对，并且允许指定请求细节和提取响应数据
        
                var httpRequest = new XMLHttpRequest();
> - 你也能重用之前的实例，但是这样的话会终止之前通过该对象挂起的任何请求。
#### 2) 请求
> - 由四部分组成：
>> - HTTP请求方法或动作；
>> - 正在请求的URL；
>> - 一个可选的请求头集合(表明请求主题的类型，以便server调用合适的程序进行处理)，其中包括身份验证的消息；
>> - 一个可选的请求主体
> - open(method, url)的第一个参数指定HTTP方法和动作，没有大小写的区分，但一般用大写。具体可以看[默默淡然的博客](https://www.cnblogs.com/liangxiaofeng/p/5798607.html)
>> - GET 用于常规请求，适用于当URL完全指定请求资源，当请求对server没有副作用以及当server的响应可缓存
>> - POST 常用于表单，请求主体中包含表单数据且这些数据需要存储到server中，这也就是所谓的副作用，同时不应该缓存使用这个方法的请求
>>>>>> ![图6-2 GET和POST的区别](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE6-2%20GET%E5%92%8CPOST%E7%9A%84%E5%8C%BA%E5%88%AB.png?raw=true)
>> - DELETE 请求服务器删除Request-URI所标识的资源。 
>> - HEAD 向服务器索要与GET请求相一致的响应，只不过响应体将不会被返回。这一方法可以在不必传输整个响应内容的情况下，就可以获取包含在响应消息头中的元信息。
>> - OPTIONS 返回服务器针对特定资源所支持的HTTP请求方法。也可以利用向Web服务器发送'*'的请求来测试服务器的功能性。
>> - PUT [跟POST方法很像，也是向服务器提交数据。但是，它们之间有不同。PUT指定了资源在服务器上的位置，而POST没有。PUT方法请求服务器去把请求里的实体存储在请求,URI（Request-URI）标识下。如果请求URI（Request-URI）指定的的资源已经在源服务器上存在，那么此请求里的实体应该被当作是源服务器关于此URI所指定资源,实体的最新修改版本。如果请求RI（Request-URI）指定的资源不存在，并且此URI被用户代理定义为一个新资源，那么源服务器就应该根据请求里的实体创建一个此URI所标识下的资源。如果一个新的资源被创建了，源服务器必须能向用户代理（user agent）发送201（已创建）响应。如果已存在的资源被改变了，那么源服务器应该发送200（Ok）或者204（无内容）响应。如果资源不能根据请求URI创建或者改变，一个合适的错误响应应该给出以反应问题的性质。实体的接收者不能忽略任何它不理解和不能实现的Content-*（如：Content-Range）头域，并且必须返回501（没有被实现）响应。如果请求穿过一个缓存（cache），并且此请求URI（Request-URI）指示了一个或多个当前缓存的实体，那么这些实体应该被看作是旧的。PUT方法的响应是不可缓存的。POST方法和PUT方法请求最根本的区别是请求URI（Request-URI）的含义不同。POST请求里的URI 指示一个能处理请求实体的资源（译注：此资源可能是一段程序，如jsp 里的servlet。此资源可能是一个数据接收过程，一个网关（gateway，译注：网关和代理的区别是：网关可以进行协议转换，而代理不能，只是起代理的作用，比如缓存服务器其实就是一个代理），或者一个单独接收注释的实体。对比而言，PUT方法请求里的URI标识请求里封装的实体一一用户代理知道URI意指什么，并且服务器不能把此请求应用于其它资源（resource）。如果服务器期望请求被应用于一个不同的URI，那么它必须发送301（永久移动）响应；用户代理可以自己决定是否重定向请求。一个单独的资  
源可能会被许多不同的URI指定。如：一篇文章可能会有一个URI指定当前版本，而这个URI区别于这篇文章其它特殊版本的URI。这种情况下，对一个通用URI的PUT请求可能会导致其资源的其它URI请求被源服务器重定义。HTTP/1.1没有定义PUT方法对源服务器的状态影响。PUT方法请求里的实体头域应该被用于资源的创建或修改。](https://blog.csdn.net/resilient/article/details/52585724)  
>> - TRACE 由于危险被禁止，回显服务器收到的请求，主要用于测试或诊断。 
>> - CONNECT 由于危险被禁止，HTTP/1.1协议中预留给能够将连接改为管道方式的代理服务器。
>> - TRACK 由于危险被禁止
> - setRequestHeader(header, value)，它可以进行多次请求，而且后者并不会覆盖前者，这些请求头主要包括：
>> - "Content-Type"，其值为MIME类型，如"text/plain"
>> - 但是自己不能指定其他请求头，如"Content-Length"，"Date"，"Referer"或者"User-Agent"等，原因是XMLHtmlRequest为了避免请求头被伪造
        
                //General
                Request URL: http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePage.html
                Request Method: GET
                Status Code: 304 
                Remote Address: 103.46.128.47:51688
                Referrer Policy: no-referrer-when-downgrade

                //Request Headers
                GET /CompatTest/BaiduHomePage.html HTTP/1.1
                Host: hblvsjtu.picp.io:51688
                Connection: keep-alive
                Cache-Control: max-age=0
                Upgrade-Insecure-Requests: 1
                User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/66.0.3359.117 Safari/537.36
                Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
                Accept-Encoding: gzip, deflate
                Accept-Language: en-US,en;q=0.9,zh-CN;q=0.8,zh;q=0.7
                If-None-Match: W/"28460-1524908730654"
                If-Modified-Since: Sat, 28 Apr 2018 09:45:30 GMTSafari/537.36
        
> - send(body) 
>> - GET请求绝对没有主体，所以send(null)或者send()
>> - POST请求通常拥有主体，同时它应该匹配使用setRequestHeader()指定的"Content-Type"头
> - 例子：
             
             var postMeg = function(msg) {
                var httpRequest = new XMLHttpRequest();
                httpRequest.open("POST", "http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePage.html");
                httpRequest.setRequestHeader("Content-Type", "text/plain;charset=UTF-8");
                httpRequest.send(msg);
             }
> - 顺序问题 先是请求方法和URL到达，然后是请求头，最后是请求主体。XMLHTMLRequest类直到调用send()方法的时候才开始启动网络。请求头必须在调用open()方法之后send()方法之前
#### 3) 响应
> - 由三部分组成：
>> - 由数字或者文字组成的状态码，用来显式请求的成功或者失败
>> - 一个响应头头集合 getResponseHeader()和getAllResponseHeaders()能查询响应头
>> - 响应主体 responseText属性能得到响应文本，从responseXML属性中能得到Document形式
> - 同步响应，只要在open(method, url, bool)的布尔值设置为false即可             
> - 响应头例子：                              
    
                //General
                Request URL: http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePage.html
                Request Method: GET
                Status Code: 304 
                Remote Address: 103.46.128.47:51688
                Referrer Policy: no-referrer-when-downgrade

                //Response Headers
                HTTP/1.1 304
                ETag: W/"28460-1524908730654"
                Date: Sun, 29 Apr 2018 02:48:21 GMT                                                           
> - 数字status或者文字statusText组成的状态码，不过我发现statusText有时会用不了，还是用数字的比较靠谱
> - 发送请求后，send()方法立即返回。而直到响应返回，前面列出的响应方法和属性才有效。loading状态下有可能触发多次readyStatechange事件来给出进度反馈
> - 为了监听readyStatechange事件，可以使用XMLHTMLRequest类的onreadyStatechange属性，当然了，也可以使用addEventListener()或者attachEvent()(除IE8及之前的版本) 
> - readyStatechange事件
     
<center>**readyState的值**</center>
>> 常量|值|含义
>> -|-|-
>> UNSENT|0|open()尚未调用
>> OPENED|1|open()已调用
>> HEADERS-RECEIVED|2|接收到头信息
>> LOADING|3|接收到响应主体
>> DONE|4|响应完成
    
> - 例子
        
                /* 原生Ajax功能
                 * 采用本地调试的时候遭遇跨域问题
                 * No 'Access-Control-Allow-Origin' header is present on the requested resource.'Ajax跨域访问解决方案
                 * 采用外网调试的时候就那没问题
                 * 发现statusText有时会用不了，还是用数字的比较靠谱 
                 */
                var getMeg = function() {
                    var httpRequest = new XMLHttpRequest();
                    httpRequest.open("GET", "http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePag.html");
                    httpRequest.setRequestHeader("Content-Type", "text/plain;charset=UTF-8");
                    httpRequest.onreadystatechange = function() {
                        console.log("HTTP请求的状态 = "+ httpRequest.readyState);
                        if(httpRequest.readyState === 4 && httpRequest.status === 200) {
                            var type = httpRequest.getResponseHeader("Content-Type");
                            if(type.match(/^text/)) {
                                console.log(httpRequest.responseText);
                            }else {
                                console.log("Content-Type is not text!");
                            }
                        }else {
                            console.log("HTTP状态码 = "+ httpRequest.status);
                            
                        }
                    }
                    httpRequest.send(null);                   
                }
                searchinput.addEventListener("click", getMeg, false);        
<center><a href="http://www.runoob.com/http/http-status-codes.html"><b>HTTP状态码分类</b></a></center>
        

>> 分类|分类描述
>> -|-
>> 1** |信息，服务器收到请求，需要请求者继续执行操作
>> 2** |成功，操作被成功接收并处理
>> 3** |重定向，需要进一步的操作以完成请求
>> 4** |客户端错误，请求包含语法错误或无法完成请求
>> 5** |服务器错误，服务器在处理请求的过程中发生了错误
        
[HTTP状态码列表](#10.2)

#### 4) 响应解码
> -  MIME类型及对应的响应方式
>> - responseText: "text/plain" "text/css" "text/html" "application/json" "application/x-www-form-urlencoded"
        
                //判断方式
                var type = htmlRequest.getResponseHeader("Content-Type");
                if(type === "application/json") {
                    //处理函数
                }
>> - responseXML: XML或者XHTML文档。这个属性的值是document对象
        
                //判断方式
                var type = htmlRequest.getResponseHeader("Content-Type");
                if(type.indexOf("XML") !== -1 && htmlRequest.responseXML) {
                    //处理函数
                }

        
<h3 id='6.3'>6.3 编码请求主体</h3>
        
#### 1) 表单编码的请求
> - MIME类型必须设置为"application/x-www-form-urlencoded"
> - 表单中的数据以名值对的形式表示，名值对之间用"&"连接，名和值之间用"="连接
> - 如
        
                name1=value1&name2=value2&name3=value3 
> - 然后对名值对执行普通的URL编码（使用十六进制转义码替换特殊字符，）
#### 2) 对对象进行编码
> - 首先是为啥要对对象进行编码呢？因为我们从表单或者其他地方得到的需要传输的数据一般都是以对象的形式存在。需要将对象转化成"name1=value1&name2=value2&name3=value3"这种格式才行。
        
                /* 对象编码模块
                  * 主要针对表单对象
                  */
                 var encodeFormData = function(data) {
                    var name;
                    var value;
                    var pair = []; //为了保存名值对；
                    if(!data) return "";
                    for(name in data) {

                        //跳过继承过来的属性
                        if(!data.hasOwnProperty(name)) continue;

                        //跳过函数
                        if(typeof data[name] === "function") continue;

                        //替换特殊符号
                        value = data[name].toString();
                        name = encodeURIComponent(name.replace("%20", "+"));
                        value = encodeURIComponent(value.replace("%20", "+"));
                        pair.push(name + "=" + value);
                    }
                    return pair.join("&");
                } 
> - 另外，关于encodeURIComponent(URIstring)函数，[W3School](http://www.w3school.com.cn/jsref/jsref_encodeURIComponent.asp)有详细的解释。或者看[dz45693的博客](https://blog.csdn.net/ma_jiang/article/details/50896048)。把字符串URIstring作为URI组件进行编码。转义用于分隔URI各个部分的标点符号。返回值为URIstring的副本，其中的某些字符将被十六进制的转义序列进行替换。该方法不会对 ASCII 字母和数字进行编码，也不会对这些 ASCII 标点符号进行编码： - _ . ! ~ * ' ( ) 。
        
                <script type="text/javascript">
                    document.write(encodeURIComponent("http://www.w3school.com.cn"))
                    document.write("<br />")
                    document.write(encodeURIComponent("http://www.w3school.com.cn/p 1/"))
                    document.write("<br />")
                    document.write(encodeURIComponent(",/?:@&=+$#"))
                </script>

                //输出
                http%3A%2F%2Fwww.w3school.com.cn
                http%3A%2F%2Fwww.w3school.com.cn%2Fp%201%2F
                %2C%2F%3F%3A%40%26%3D%2B%24%23
> - 那至于为什么要对URI进行编码呢？[hbiao68的专栏](https://blog.csdn.net/hbiao68/article/details/17113843)给出了答案："为什么需要Url编码，通常如果一样东西需要编码，说明这样东西并不适合传输。原因多种多样，如Size过大，包含隐私数据，对于Url来说，之所 以要进行编码，是因为Url中有些字符会引起歧义。例如Url参数字符串中使用key=value键值对这样的形式来传参，键值对之间以&符号分隔，如/s?q=abc&ie=utf-8。如果你的value字符串中包含了=或者&,那么势必会造成接收Url的服务器解析错误，因此必须将引起歧义的&和=符号进行转义，也就是对其进行编码。 又如，Url的编码格式采用的是ASCII码，而不是Unicode，这也就是说你不能在Url中包含任何非ASCII字符，例如中文。否则如果客户端浏览器和服务端浏览器支持的字符集不同的情况下，中文可能会造成问题。"
#### 3) 对表单数据进行传输
> - 一个简单的POST请求
        
                // 一个简单的POST请求
                var MesPost = function(URL, data, callBack) {
                    var request = new XMLHttpRequest;
                    request.open("POST", URL);
                    request.onreadystatechange = function() {
                        if(request.readyState === 4 && request.status === 200 && callBack) {
                            callBack(request);
                        }
                    }
                    request.setRequestHeader("Content-Type", "application/x-www-form-urlencoded");
                    request.send(encodeFormData(data));
                }
> - 一个简单的GET请求
        
                // 一个简单的GET请求
                // 如果没有显式地设置Content-Type头，那么XHR会自动补上
                // "ext/plain; charset=UTF-8"头
                var MesPost = function(URL, data, callBack) {
                    var request = new XMLHttpRequest;
                    request.open("GET", URL + "?" + encodeFormData(data));
                    request.onreadystatechange = function() {
                        if(request.readyState === 4 && request.status === 200 && callBack) {
                            callBack(request);
                        }
                    }
                    request.send(null);
                }
         

<h3 id='6.4'>6.4 HTTP进度事件</h3>
        
#### 1) 事件集
> - XHR2规范中定义了许多事件集，这就意味着不需要总是先检查XMLHtmlRequest.readyState的值
>> - 比如调用send()的时候触发单个loadstart事件。
>> - 当加载服务器响应的时候，发生progress事件，通常每隔50毫秒左右，可以使用这些事件来反馈请求的进度。progress事件对象有几个比较好用的属性
>>> - lengthComputable 如果从"Content-length"头得知传输数据的整体长度(单位是字节)不为0，此时其值为true，否则为false;
>>> - loaded 目前传输的字节数；
>>> - total 从"Content-length"头得知传输数据的整体长度(单位是字节)
        
                /* HTML进度模块
                 */
                 var progressModuel = function(ele, htmlRequest) {
                    if(typeof ele !== "string") {
                        throw new Error("类型错误"); 
                    }else {
                        var element = document.getElementById(ele);
                        if("onprogress" in htmlRequest) {
                            //支持progress事件；
                            htmlRequest.onprogress = function(e) {
                                if(e.lengthComputable) {
                                   element.value = Math.round(100*e.loaded/e.total) + "% complete";
                                   console.log("progressModuelfunction");
                                }
                             }
                        }
                    } 
                 }
>> - 当事件完成的时候触发**load事件**。HTTP请求无法完成有3中情况，对应着三种事件：请求超时(触发timeout事件)；请求中止(触发abort事件)；由于太多重定向造成的网络错误(触发error事件)。目前会发生而且仅会触发load事件，timeout事件，abort事件，error事件的其中一个。当上面任意一个事件结束的时候，浏览器会触发**loadend事件**；
#### 2) 上传文件
> - 参见[芭蕉扇的博客](https://www.cnblogs.com/tianyuchen/p/5594641.html)
> - 需要后端的处理，具体就是在url那里下功夫
                
                <!DOCTYPE html>
                <html>
                <head>
                <meta charset="UTF-8">
                    <title>XMLHttpRequest上传文件进度实现</title>
                    <script type="text/javascript">
                        var xhr;
                        var ot;//
                        var oloaded;
                        //上传文件方法
                        function UpladFile() {
                            var fileObj = document.getElementById("file").files[0]; // js 获取文件对象
                            var url = "uploadFile"; // 接收上传文件的后台地址 
                            
                            var form = new FormData(); // FormData 对象
                            form.append("mf", fileObj); // 文件对象
                            
                            xhr = new XMLHttpRequest();  // XMLHttpRequest 对象
                            xhr.open("post", url, true); //post方式，url为服务器请求地址，true 该参数规定请求是否异步处理。
                            xhr.onload = uploadComplete; //请求完成
                            xhr.onerror =  uploadFailed; //请求失败
                            xhr.upload.onprogress = progressFunction;//【上传进度调用方法实现】
                            xhr.upload.onloadstart = function(){//上传开始执行方法
                                ot = new Date().getTime();   //设置上传开始时间
                                oloaded = 0;//设置上传开始时，以上传的文件大小为0
                            };
                            xhr.send(form); //开始上传，发送form数据
                        }
                        //上传进度实现方法，上传过程中会频繁调用该方法
                        function progressFunction(evt) {
                            
                             var progressBar = document.getElementById("progressBar");
                             var percentageDiv = document.getElementById("percentage");
                             // event.total是需要传输的总字节，event.loaded是已经传输的字节。如果event.lengthComputable不为真，则event.total等于0
                             if (evt.lengthComputable) {//
                                 progressBar.max = evt.total;
                                 progressBar.value = evt.loaded;
                                 percentageDiv.innerHTML = Math.round(evt.loaded / evt.total * 100) + "%";
                             }
                            
                            var time = document.getElementById("time");
                            var nt = new Date().getTime();//获取当前时间
                            var pertime = (nt-ot)/1000; //计算出上次调用该方法时到现在的时间差，单位为s
                            ot = new Date().getTime(); //重新赋值时间，用于下次计算
                            
                            var perload = evt.loaded - oloaded; //计算该分段上传的文件大小，单位b       
                            oloaded = evt.loaded;//重新赋值已上传文件大小，用以下次计算
                        
                            //上传速度计算
                            var speed = perload/pertime;//单位b/s
                            var bspeed = speed;
                            var units = 'b/s';//单位名称
                            if(speed/1024>1){
                                speed = speed/1024;
                                units = 'k/s';
                            }
                            if(speed/1024>1){
                                speed = speed/1024;
                                units = 'M/s';
                            }
                            speed = speed.toFixed(1);
                            //剩余时间
                            var resttime = ((evt.total-evt.loaded)/bspeed).toFixed(1);
                            time.innerHTML = '，速度：'+speed+units+'，剩余时间：'+resttime+'s';
                               if(bspeed==0)
                                time.innerHTML = '上传已取消';
                        }
                        //上传成功响应
                        function uploadComplete(evt) {
                         //服务断接收完文件返回的结果
                         //    alert(evt.target.responseText);
                             alert("上传成功！");
                        }
                        //上传失败
                        function uploadFailed(evt) {
                            alert("上传失败！");
                        }
                          //取消上传
                        function cancleUploadFile(){
                            xhr.abort();
                        }
                    </script>
                </head>
                <body>
                    <progress id="progressBar" value="0" max="100" style="width: 300px;"></progress>
                    <span id="percentage"></span><span id="time"></span>
                    <br /><br />
                    <input type="file" id="file" name="myfile" />
                    <input type="button" onclick="UpladFile()" value="上传" />
                    <input type="button" onclick="cancleUploadFile()" value="取消" />
                </body>
                </html> 

                
------      
         
        
<h2 id='7'> 七、客户端储存</h2>
<h3 id='7.1'>7.1 客户端储存简介</h3>
        
#### 1) 遵循同源策略
> - 不同站点的页面是无法相互读取对方存储的数据，而同一站点的不同页面之间是可以相互共享存储数据的
#### 2) 分类
> - Web存储 包括localStorage对象和sessionStorage对象，最初作为HTML5的一部分被定义为API的形式，实际上它们都是持久化关联数组(Storage对象)，同时也是window对象的属性；
> - cookie  早期的客户端储存机制，但是风评很差，document的属性;
> - IE User Data 巨硬公司早期的专属客户端存储机制；
> - 离线web应用 就是把整个Web应用方法客户端那里，妈妈再也不用担心我断网；
> - Web数据库 各家浏览器厂商并不打算实现它
> - 文件系统API
        
<h3 id='7.2'>7.2 localStorage和sessionStorage</h3>
        
#### 1) 储存的有效期和作用域不同
> - 拥有getItem(), setItem(), removeItem(), clear()等方法；
> - 拥有类似数组一样的[]方法和.方法；
#### 2) localStorage
> - 永久性，除非Web应用刻意删除，或者用户自己删除，否则一直会存在于用户的电脑
> - 作用域限定于相同的文档源和浏览器供应商。这意味着chrome和Firefox的不能相互访问；
                
                localStorage.setItem("sex", "male");
                console.log(localStorage.getItem("sex"));
>>>>>> ![图7-1 文档源](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE7-1%20%E6%96%87%E6%A1%A3%E6%BA%90.png?raw=true)
        
#### 3) sessionStorage
> - 暂时性
> - 同源而且是同一个标签页的顶级窗口，也就是说在一个标签页里面不同的iframe元素窗口中的sessionStorage数据是可以共享的;
        
                
                sessionStorage.setItem("id", 116020910160);
                console.log(sessionStorage.getItem("id"));
#### 4) 存储API
> - setItem();
> - getItem();
> - removeItem();
> - clear();
> - length
> - key() 枚举名字
> - 如果存储的是数组或者对象的时候，获取该对象或者数组的时候也要求获取的是该对象的副本，以确保以获取对象的改动不会影响到存储的对象。 
>>>>>> ![图7-2 存储API](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE7-2%20%E5%AD%98%E5%82%A8API.png?raw=true) 
        
                // 识别出使用的是哪类存储机制
                var memory = window.localStorage || 
                            (window.UserDataStorage && new UserDataStorage()) ||
                            new cookieStorage();
                // 然后在对应的机制中查询数据
                var name = memory.getItem("username");
#### 5) 存储事件
> - localStorage和存储事件都是采用广播机制的，浏览器会对目前正在访问同样站点的所有窗口发送消息
> - 与存储事件相关的5个非常重要的特性
>> - key
>> - newValue
>> - oldValue
>> - storageArea
>> - url
        
<h3 id='7.3'>7.3 cookie</h3>
        
#### 1) 安全性
> - JS中使用cookie不会采用任何加密机制，因此它们是不安全的。但是使用https来传输的话cookie数据是安全的，不过这和cookie本身无关，而和cookie本身无关，而和https:协议相关
> - 与安全性相关的属性就是secure，它是一个布尔值，一旦cookie被认为是安全的，那只有https等安全的协议才能传递它。
#### 2) 操作API
> - 没有专门的API，所以需要直接通过以特殊格式的字符串形式读写Document对象cookie属性来完成。
> - 有效期和作用域都是通过cookie属性来分别指定 
#### 3) 有效期
> - 默认是整个浏览器进程的生命周期
> - 可以通过设置max-age属性来修改
#### 4) 作用域
> - 通过文档源和文档路径来确定的
> - 通过cookie的path和domain属性也可以配置
> - 默认与创建它的页面有关，并对该Web页面以及和该Web页面同目录或者子目录的其他Web页面可见
> - 但是也可以修改，通过修改path路径，如果将path路径设置为"/"，那么该cookie对该台服务器上的所有页面都是可见的，这就相当于跟localStorage拥有相同的作用域
> - 如果一个Web页面想要读取同一站点其他页面的cookie，只要简单的将其他页面以隐藏的iframe元素的形式加载进来，随后读取对应文档的cookie即可。但是由于同源策略的限制，只能对于同源的服务器这样做。
> - 如果想要跨域的话，那么就需要设置cookie的domain属性，比如在catalog.example.com域下的一个页面创建了一个cookie，并将其path设置为“/”，其domain设置为.example.com，那么这个cookie对catalog.example.com，order.example.com，以及任何其他example.com域下的任何服务器都可见。
#### 5) 保存cookie
> - cookie是document的属性
        
                document.cookie = "version=" + encodeURIComponent(document.lastModified);
> - 名值对中不允许包含分号，逗号和空白符，因此在存储前一般采用全局函数encodeURIComponent()对值及进行编码
> - 延长有效期，单位是秒
        
                name=value; max-age = seconds;
> - 还有其他特性，使用字符串拼接在其后即可
        
                name=value; max-age = seconds; path=path; domain=domain; sercue
> - 要改变cookie的值，需要相同的名字，路径和域，有效期可改可不改；
> - 要删除一个cookie，也需要相同的的名字，路径和域，然后其值指定为任意非空值，并且将max-age属性指定为0，只要将cookie的过期时间设置为负值，cookie就会直接消失。
        
                /* cookie保存
                 */
                var saveCookie = function(name, value, maxAge, domain, path) {
                    if(name && value) {
                        cookie = encodeURIComponent(name) + "=" +encodeURIComponent(value) + "; ";
                        cookie += "max-age=" + maxAge + "; ";
                        if(domain) cookie += "domain=" + domain + "; ";
                        if(path) cookie += "path=" + path + "; ";
                        document.cookie = cookie;
                    }
                } 
                
                saveCookie("name", "lvhongchao", 10, ".hblvsjtu.picp.io", "/");
                saveCookie("name", "lvhongchao", 0, ".hblvsjtu.picp.io", "/");
#### 6) 读取cookie
> - 目前的情况下只能读取名值对，都不了域和路径；
> - 注意分号后面还有一个空格；
                
                /* cookie读取
                 */
                 var readCookie = function() {
                    var cookie = {};
                    var all = document.cookie;
                    if(all === "") {
                        console.log("the cookie is null");
                        return;
                    }
                    var list = all.split("; ");
                    for(var i=0; i<list.length; i++) {
                        var pairs = list[i];
                        var p = pairs.indexOf("=");
                        var name = pairs.substring(0, p);
                        var value = pairs.substring(p+1);
                        value = decodeURIComponent(value);
                        cookie[name] = value;
                        console.log(name + " = " +value);
                    }
                    return cookie;
                 }

                readCookie();

#### 7) cookie的局限性
> - 标准规定浏览器的保存不超过300个cookie；
> - 每个服务器保存不超过20个；
> - 每个cookie大小不超过4KB；
        
<h3 id='7.4'>7.4 应用程存储和离线Web应用</h3>
                
#### 1) 步骤
> - 网站的每一个html页面都必须设置html元素的manifest属性。Must to do；
> - 在你的整个网站应用中，只能有一个cache.manifest文件（建议放在网站根目录下）；
> - 部分浏览器（如IE8-）不支持HTML5离线缓存；
> - “#” 开头的注释行可满足其他用途。应用的缓存会在其 manifest 文件更改时被更新。如果您编辑了一幅图片，或者修改了一个 JavaScript 函数
> - 真正运行或测试离线web应用程序的时候，需要对服务器进行配置，让服务器支持text/cache-manifest这个MIME类型（在h5中规定manifest文件的MIME类型是text/cache-manifest）。
#### 2) 缓存的更新
> - 当一个web应用从缓存中载入的时候，所有与之相关的文件也是直接从缓存中获取。在线状态下，浏览器会异步地检查清单文件是否有更新。
> - 如果有更新，新的清单文件以及清单中的列举的所有文件都会下载下来重新保存到程序缓存中。但要注意浏览器只是检查清单文件，而不会检查缓存的文件是否有更新，如果修改一个缓存的js文件，并且要想让该文件生效，就必须去更新下清单文件。由于应用程序依赖的文件列表其实并没有变化，因此最简单的方式就是更新版本。代码如下：
        
                CHCHE MANIFEST  
                CACHE:  
                #version 1.0 
                 myapp.html  
                 myapp.css  
                 myapp.js  
#### 3) applicationCache对象
> - 属于window的属性
> - 拥有显式更新缓存的方法
>> - update() 如果检测到相同的一份缓存清单，那么还是会跟原来的一样
>> - swapCache() 告诉浏览器弃用老的缓存而采用新的缓存，但是不会去主动联网来获取新的缓存，在updateready事件，或者onobsolete事件中采用意义(立即弃用废弃的缓存，而从网络中获取) 但是这种方法好像已经被标准所弃用
#### 4) navigator.online
> - 该属性可以检验浏览器是否在线 
> - true表示在线
> - false表示离线
#### 5) 缓存状态
> - 缓存的状态可以通过window.applicationCache.status获得，其状态主要包括如下6种：
>> - UNCACHED=0;//未缓存(应用程序没有设置manifest属性：未缓存)  
>> - IDLE=1;//空闲状态(清单文件已经检查完毕，并且已经缓存了最新的应用程序)    
>> - CHECKING=2;//检查中(浏览器正在检查清单文件)    
>> - DOWNLOADING=3;//下载中(浏览器正在下载并缓存清单中列举的所有文件)  
>> - UPDATEREADY=4;//更新准备中(已经下载和缓存了最新版的应用程序)  
>> - OBSOLETE =5;//过期状态(清单文件不存在，缓存将被清除) 
#### 6) 优缺点，[来自知乎用户黎博的回答](https://www.zhihu.com/question/35130316)
> - 简单来说，不好用。来分析下manifest的优缺点优点可以离线运行可以减少资源请求可以更新资源缺点更新的资源，需要**二次刷新**才会被页面采用不支持增量更新，只有manifest发生变化，所有资源全部重新下载一次缺乏足够容错机制，当清单中任意资源文件出现加载异常，都会导致整个manifest策略运行异常。
> - **全量加载**和**二次刷新**这两个缺点就已经够严重了。我们再来看看其优点是不是真的那么好用。
> - 1.离线运行对于普通页面来说，离线运行没什么用；对于webapp来说，这个特性还不错；对于hybird app来说，也没什么用。
> - 2.减少资源请求HTTP协议的Cache-Control和Expires就也能在缓存有效期内，不再发送资源请求
> - 3.可以更新资源manifest是文件被更新后，全量更新缓存。而改用HTTP协议的缓存方案，只需要对资源文件引用的URL做少许变动即可刷新缓存，例如补个时间戳参数一个manifest相关的坑，虽然也能填：如何不让html5 app cache的manifest缓存当前页面?

作者：黎博
链接：https://www.zhihu.com/question/35130316/answer/91006638
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


                //html文件
                <<!DOCTYPE html>
                <html manifest="myapp.appcache">
                    <head>
                        <title></title>
                    </head>
                    <body>
                    </body>
                    <script type="text/javascript">
                        /* 下面所有的事件处理程序都使用此函数来显示状态消息  
                         * 由于都是通过调用status函数来显示状态，因此所有处理程序都返回false来阻止浏览器显示其默认状态消息
                         */  
                        function status(msg){  
                            console.log(msg); //同时在控制台输出此消息，便于调试  
                        } 

                        /* 每当应用程序载入的时候，都会检查该清单文件  
                         * 也总会首先触发"checking"事件
                         */  
                        window.applicationCache.onchecking = function(){  
                            status("checking for a new version.");  
                            return false;  
                        }  

                        /* 如果没有改动，同时应用程序也已经缓存了  
                         * "noupdate"事件被触发，整个过程结束 
                         */ 
                        window.applicationCache.onnoupdate = function(){ 
                            status("The application has been cached"); 
                        } 

                        /* 如果还未缓存应用程序，或者清单文件有改动  
                         * 那么浏览器会下载并缓存清单中的所有资源  
                         * 触发"downloading"事件，同时意味着下载过程开始
                         */  
                        window.applicationCache.ondownloading = function(){  
                            status("Downloading new version");  
                            window.progresscount = 0;  
                            return false;  
                        } 

                        /* 在下载过程中会间断性触发"progress"事件  
                         * 通常是在每个文件下载完毕的时候 
                         */
                        window.applicationCache.onprogress = function(e){  
                            varprogress = "";  
                            if(e && e.lengthComputable)  
                                   progress = " "+Math.round(100*e.loaded/e.total)+"%"  
                            else  
                                   progress = "("+(++progresscount)+")"  
                            return false;  
                        }

                        /* 当下载完成并且首次将应用程序下载到缓存中时
                         * 浏览器会触发"cached"事件
                         */  
                        window.applicationCache.oncached = function(e){  
                            status("This application has been cached before");  
                            return false;  
                        }  
                           
                        /* 当下载完成并将缓存中的应用程序更新后，浏览器会触发"updaterady"事件  
                         * 要注意的是：触发此事件的时候，用户任然可以看到老版本的应用程序
                         */  
                        window.applicationCache.onupdateready = function(e){  
                            var reload = confirm("A new version has been downloaded. Would you like to Reload to run it?");
                    if(reload) {
                            applicationCache.swapCache();
                            if(navigator.onLine) status("navigator.onLine"); 
                            window.location.reload(); 
                    }
                    return false;   
                        }  
                           
                        /* 如果浏览器处于离线状态，检查清单列表失败，则会触发"error"事件  
                         * 当一个未缓存的应用程序引用一个不存在的清单文件，也会触发此事件
                         */ 
                        window.applicationCache.onerror = function(e){  
                            status("Couldn’t load manifest or cache application");  
                            return false;  
                        }  
                           
                        /* 如果一个缓存的应用程序引用一个不存在的清单文件，会触发"obsolete"  
                         * 同时将应用从缓存中移除之后不会从缓存而是通过网络加载资源
                         */  
                           window.applicationCache.onobsolete = function(e){  
                                status("This application is no longer cached. Reload to get the latest version from thenetwork.");  
                                return false;  
                           }  
                    </script>
                    </script>
                </html>

        
                //manifest.appcache文件
                CACHE MANIFEST
                # version 2018-05-01 15:34
                CACHE:
                BaiduHomePage.html
                BaiduHomePage.css
                jquery-3.3.1.js
                myIcon.ico
                picture/surcue2.png
                picture/zhuazi2.png
                picture/mylogo.png

                FALLBACK:
                BaiduHomePage.html

                NETWORK:

                //调试结果：
                checking for a new version.
                BaiduHomePage.html:1 Application Cache Downloading event
                BaiduHomePage.html:627 Downloading new version
                BaiduHomePage.html:1 Application Cache Progress event (0 of 7) http://hblvsjtu.picp.io:51688/CompatTest/myIcon.ico
                BaiduHomePage.html:1 Application Cache Progress event (1 of 7) http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePage.css
                BaiduHomePage.html:1 Application Cache Progress event (2 of 7) http://hblvsjtu.picp.io:51688/CompatTest/picture/mylogo.png
                BaiduHomePage.html:1 Application Cache Progress event (3 of 7) http://hblvsjtu.picp.io:51688/CompatTest/picture/surcue2.png
                BaiduHomePage.html:1 Application Cache Progress event (4 of 7) http://hblvsjtu.picp.io:51688/CompatTest/jquery-3.3.1.js
                BaiduHomePage.html:1 Application Cache Progress event (5 of 7) http://hblvsjtu.picp.io:51688/CompatTest/picture/zhuazi2.png
                BaiduHomePage.html:1 Application Cache Progress event (6 of 7) http://hblvsjtu.picp.io:51688/CompatTest/BaiduHomePage.html
                BaiduHomePage.html:1 Application Cache Progress event (7 of 7) 
                BaiduHomePage.html:1 Application Cache UpdateReady event
                BaiduHomePage.html:627 A new version has been downloaded. Reload to run it //所以需要二次刷新      

[3、permanote.js](#10.3)       
            
        
------      
    
        
<h2 id='八'>八、HTML5 API</h2>        
<h3 id='8.1'>8.1 地理位置</h3>    
        
#### 1) 三个属性
> - navigator.geolocation.getCurrentPosition() 获取用户当前的位置；
> - navigator.geolocation.watchPosition() 不断监视用户当前的位置，一旦用户位置发生了改变，就会调用指定的回调函数；
> - navigator.geolocation.clearPosition() 停止监视用户当前的位置，传递给此方法的参数应当是调用watchPosition()方法获得的返回值；
        
                /* 地理位置获取模块
                 * 好像只有本地调试模式下才能获得数据
                 * 在外网下调试由于安全性等原因不能获取
                 */
                var getPosition = function() {
                    if(navigator.geolocation) {
                        navigator.geolocation.getCurrentPosition(function(pos){
                            var latitude = pos.coords.latitude;
                            var longitude = pos.coords.longitude;
                            console.log("Your position: latitude = " + latitude);
                            console.log("Your position: longitude = " + longitude);
                        });
                    }else {
                        console.log("navigator.geolocation doesn’t work!");
                    }
                }
                getPosition();

    
<h3 id='8.2'>8.2 历史记录管理</h3>    
        
#### 1) 结构性复制structured clone
> - 对一个对象进行深拷贝或者深复制，进而递归地复制所有嵌套对象或者数组的内容
> - 比如我们熟悉的序列化JSON.stringgfy和JSON.parse
>>>>>> ![图8-1 结构性复制](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE8-1%20%E7%BB%93%E6%9E%84%E6%80%A7%E5%A4%8D%E5%88%B6.png?raw=true)
> - 
    
<h3 id='8.3'>8.3 跨域消息传递</h3>    
        
#### 1) 简介
> - 一般来讲，一个窗口或者一个标签中运行的代码其他窗口中完全无法识别。
> - 但是也有例外，比如当用脚本显式打开一个新窗口或者在嵌套的窗体中运行的时候，多个窗口或者嵌套的窗体之间是可以互相识别的。如果这些窗口或者嵌套的窗体是同源的，那么还可以相互进行交互和操作对方的文档。
#### 2) postMessage() 具体可以看[谦行的博客](https://www.cnblogs.com/dolphinX/p/3464056.html),
> - 这种技术叫"跨文档消息传递"，定义在window对象上，而非document文档对象，允许非同源的脚本的调用；
> - 异步消息传递，所有主流的浏览器(包括IE8和更新的版本)都已经实现了该通信机制
> - postMessage(data,origin)方法接受两个参数
>> - data:要传递的数据，html5规范中提到该参数可以是JavaScript的任意基本类型或可复制的对象，然而并不是所有浏览器都做到了这点儿，部分浏览器只能处理字符串参数，所以我们在传递参数的时候需要使用JSON.stringify()方法对对象参数序列化，在低版本IE中引用json2.js可以实现类似效果。
>> - origin：字符串参数，指明目标窗口的源，协议+主机+端口号[+URL]，URL会被忽略，所以可以不写，这个参数是为了安全考虑，postMessage()方法只会将message传递给指定窗口，当然如果愿意也可以建参数设置为"*"，这样可以传递给任意窗口，如果要指定和当前窗口同源的话设置为"/"。
> - 发送消息页面：http://test.com/index.html       
        
                /* 我们可以在http://test.com/index.html
                 * 通过postMessage()方法向跨域的iframe页面http://lsLib.com/lsLib.html传递消息
                 */
                <script type="text/javascript">
                    window.onload=function(){
                        window.frames[0].postMessage('getcolor','http://lslib.com');
                    }
                </script>
                <div style="width:200px; float:left; margin-right:200px;border:solid 1px #333;">
                    <div id="color">Frame Color</div>
                </div>
                <div>
                    <iframe id="child" src="http://lsLib.com/lsLib.html"></iframe>
                </div>
> - 接收消息页面：http://lslib.com/lslib.html
        
                window.addEventListener('message',function(e){
                    if(e.source!=window.parent) return;
                    var color=container.style.backgroundColor;
                    window.parent.postMessage(color,'*');
                },false);
> - 主页面接收消息
        
                window.addEventListener('message',function(e){
                    var color=e.data;
                    document.getElementById('color').style.backgroundColor=color;
                },false);
#### 3) 有几个重要属性
> - data：顾名思义，是传递来的message
> - source：发送消息的窗口对象
> - origin：发送消息窗口的源（协议+主机+端口号）
    
<h3 id='8.4'>8.4 Web Worker 详细的可以看<a href="https://blog.csdn.net/ningtt/article/details/74980291">ningtt的博客</a></h3>    
        
#### 1) 简介
> - 运行在一个自包含的执行环境，无法访问Window对象和Document对象，和主线程之间的通信也是通过异步消息传递机制来实现的
> - 只要message事件有可能触发，那么它将永远不会退出，但是，如果Worker一直没有监听到消息，那么一直到所有任务相关的回调函数都调用以及再也没有挂起的任务，它就会退出；
#### 2) Worker对象
> - 需要创建，把js脚本的URL传递进去作为参数，且该脚本与文档是同源的
        
                var loader = new Worker(url);
> - 要注意的是，Worker对象的postMessage()是没有参数的，这一点跟Window对象的postMessage()不同(它有两个参数)，        
> - 简而言之，就是允许JavaScript创建多个线程，但是子线程完全受主线程控制，且不得操作DOM。
从而，可以用webWorker来处理一些比较耗时的计算。
> - 使用web worker主要分为以下几部分
>> - WEB主线程:
        
        1.通过 worker = new Worker( url ) 加载一个JS文件来创建一个worker，同时返回一个worker实例。
        2.通过worker.postMessage( data ) 方法来向worker发送数据。
        3.绑定worker.onmessage方法来接收worker发送过来的数据。
        4.可以使用 worker.terminate() 来终止一个worker的执行。
>> - worker新线程：
         
        1.通过postMessage( data ) 方法来向主线程发送数据。
        2.绑定onmessage方法来接收主线程发送过来的数据。                    
> - postMessage(data) 子线程与主线程之间互相通信使用方法，传递的data为任意值
> - terminate() 主线程中终止worker，此后无法再利用其进行消息传递。注意：一旦terminate后，无法重新启用，只能另外创建。
        
                worker.terminate();
> - message  当有消息发送时，触发该事件。且，消息发送是双向的，消息内容可通过data来获取。
message使用，可见terminate中的demo
> - error 出错处理。且错误消息可以通过e.message来获取worker.js执行的上下文，与主页面html执行时的上下文并不相同，最顶层的对象并不是window，woker.js执行的全局上下文，是个叫做WorkerGlobalScope的东东，所以无法访问window、与window相关的DOM API，但是可以与setTimeout、setInterval等协作。
#### 3) Worker作用域——WorkerGlobalScope全局对象
> - 由于Worker指定的代码运行在全新的JS环境中
> - WorkerGlobalScope全局对象则表示了该新的运行环境
> - WorkerGlobalScope全局对象在某种意义上讲大于核心的JS全局对象，小于整个客户端的Window对象；
> - 在Worker中的JS代码内调用的postMessage()方法会触发Worker外部的一个message事件，而Worker外部传递的消息会转换成一个事件，并传递给onmessage事件处理程序；
> - 要注意的是，WorkerGlobalScope全局对象是一个供Worker使用的全局对象，因此该对象上的postMessage()方法和onmessage属性在worker代码中使用的时候，看起来就像是全局函数和全局变量；
> - self 我们可以使用 WorkerGlobalScope 的 self 属性来或者这个对象本身的引用
> - location location 属性返回当线程被创建出来的时候与之关联的 WorkerLocation对象，它表示用于初始化这个工作线程的脚步资源的绝对URL，即使页面被多次重定向后，这个 URL 资源位置也不会改变。
> - close 关闭当前线程，与terminate作用类似
> - XMLHttpRequest 有了它，才能发出Ajax请求
> - setTimeout/setInterval以及addEventListener/postMessage
> - importScripts()方法，这是一个同步的方法，以用来加载其他库，接受一个或者多个URL参数，相对地址的参考是传递给Worker构造函数的URL，如：
        
                importScripts("collections/Set.js", "collections/Map.js");
#### 4) 例子
> - workerTest.js 在JS中不需要Worker.onmessage或者Worker.postMessage，直接上来就可以用
                
                /**
                 * 
                 * @authors LvHongbin
                 * @date    2018-05-02 14:43:01
                 * @version 1.0
                 * @workerTest.js
                 */

                onmessage = function(e) {
                    console.log("I have got the message e.data = " + e.data);
                    if(e.data) postMessage(fib(e.data));
                }

                var fib = function(n) { 
                    return n<=2?n:fib(n-1) + fib(n-2);  
                }

> - HTML文档
                
                <!DOCTYPE HTML>
                <html>
                <head>
                <meta http-equiv="Content-Type" content="text/html; charset=utf-8"/>
                <title>web worker fibonacci</title>
                    <script type="text/javascript">

                        /* worker moduel
                         * 两种接受消息的方法都可以
                         * 发送消息和接受消息的语句不要嵌套
                         * 但是在workerTest.js里面可以嵌套
                         */ 
                        var worker = new Worker("workerTest.js");
                        worker.postMessage(40);
                        //worker.addEventListener("message", function(e) {console.log("The worker fib result = " + e.data);}, false);
                        worker.onmessage = function(e) {console.log("The worker fib result = " + e.data);};  
                    </script>
                </head>
                <body>
                </body>
                </html>

#### 5) 优缺点：
> - 优点：
>> - 1.可以加载一个JS进行大量的复杂计算而不挂起主进程，并通过postMessage，onmessage进行通信
>> - 2.可以在worker中通过importScripts(url)加载另外的脚本文件
>> - 3.可以使用 setTimeout(), clearTimeout(), setInterval(), and clearInterval()
>> - 4.可以使用XMLHttpRequest来发送请求
>> - 5.可以访问navigator的部分属性
> - 缺点：
>> - 1.不能跨域加载JS
>> - 2.worker内代码不能访问DOM
>> - 3.各个浏览器对Worker的实现不大一致，例如FF里允许worker中创建新的worker,而Chrome中就不行
>> - 4.不是每个浏览器都支持这个新特性
        
<h3 id='8.5'>8.5 类型化数组和ArrayBuffer</h3>    
        
#### 1) 类型化数组
> - 元素都是数字，使用构造函数创建类型化数组对象的时候，就决定了数字的类型(有符号或者无符号，整数或者浮点数)和大小
> - 有固定的长度
> - 创建数组的时候，数组的元素总默认为0
> - 一旦创建后，跟其他数组的使用差不多
> - 为了高效，采用底层系统硬件的原生顺序，低位优先(little-endian)
> - 比如：
>> - Int8Array() 有符号字节
>> - UInt8Array() 无符号字节
>> - Int16Array() 有符号16位短整数
>> - UInt16Array() 无符号16位短整数
>> - Int32Array() 有符号32位整数
>> - UInt32Array() 无符号32位整数
>> - Float32Array() 32位浮点数值
>> - Float64Array() 64位浮点数值，JS中的常规数字
        
                var int8 = new UInt8Array(8); //分配8个字节；
> - 类型化数组还有一个subarray(n1, n2)的方法，返回索引n1 <= n < n2的数的子数组，而且该子数组last3作为原数组ints的一部分存在，同命运共呼吸，一改全都改。可以说只是返回当前数组的一个新的视图
        
                var ints = new Int16Array([0, 1, 2, 3, 4]);
                var last3 = ints.subarray(ints.length-3, ints.length); //取最后三个
#### 2) ArrayBuffer
> - 每个类型化数组都有与基本缓冲区相关的三个属性
>> - last3.buffer   // =>返回一个ArrayBuffer对象 
>> - last3.buffer == ints.buffer    // =>true: 两者在同一个缓冲区的视图
>> - last3.byteOffset   // =>此视图从基本缓冲区的第4个字节开始 16/8*2=4
>> - last3.bytelength   // =>6:此视图有6字节 16/8*3=6
>> - last3.buffer.bytelength   // =>10:基本缓冲区有10字节 16/8*5=10
> - ArrayBuffer对象自己不是一个类型化数组，可以像数组那样操纵ArrayBuffer，但是就是不能访问缓冲区的字节
        
                var buf = new ArrayBuffer(1024*1024) //1MB
                var asbytes = new UInt8Array(buf) //视为字节
                var asints = new Int32Array(buf) //视为32位有符号整数
> - ArrayBuffer是一块内存，或者说是带类型的高速数组，比如var buf = new ArrayBuffer(1024)，就等于开辟了一块1kb大小的内存，但是你不能通过buf变量的索引去操作这块内存，比如console.log(buf[0])得到的是undefined，如果buf[0]=77,进行赋值操作，只是在buf对象上添加了一个属性名为‘0’的属性，并没有改变内存块中第一个字节的数据，如果想操作内存块中的数据，可以通过var int8= new Int8Array(buf)然后通过int8[0]=12;来操作这块内存中的数据，也可以用Int16Array(buf)，Int32Array(buf)等，传入的是同一块内存块的引用则操作同一块内存块，剩下的自己理解吧。
作者：李建万
链接：https://www.zhihu.com/question/30401979/answer/133686569
来源：知乎
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
> - 由于类型化数组采用的是小端系统，所以ArrayBuffer也只好跟随
>>>>>> ![图8-2 大小端判断](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE8-2%20%E5%A4%A7%E5%B0%8F%E7%AB%AF%E5%88%A4%E6%96%AD.png?raw=true)
        
#### 3) DataView类
> - 构造函数new DataView(buffer);
        
                var data;   //假设这是来自网络的ArrayBuffer
                var view = DataView(data);
> - setInt(offset, num, boolean)方法，第一个参数是字节偏移量，即从第几个值开始写起，第二个参数是指定要写入的值，第三个布尔量指的是大小端的选择，true为小端，false为大端，默认是大端。
> - 和getInt(offset, boolean)的方法，第一个参数是字节偏移量，即从第几个值开始读起，第二个参数是大小端的选择，true为小端，false为大端，默认是大端看。
                
                // create an ArrayBuffer with a size in bytes
                var buffer = new ArrayBuffer(16);

                // Create a couple of views
                var view1 = new DataView(buffer);
                var view2 = new DataView(buffer,12,4); //from byte 12 for the next 4 bytes
                view1.setInt8(12, 42); // put 42 in slot 12

                console.log(view2.getInt8(0));
                // expected output: 42
<h3 id='8.6'>8.6 Blob</h3>    
        
#### 1) 定义
> - 对大数据块的不透明引用或者句柄，名字来源于SQL数据库，表示"二进制大对象"(Binary Large Object)。在JS中，Blob通常表示二进制数据
> - 不透明，能对它操作的就只有获取它们的大小(以字节为单位)，MIME类型；
> - Blob是很大的数据块，如果不事先把它分割成小的数据块，后面很难把它放到主存中，同时正是由于需要操作大数据快，需要异步的API
>>>>>> ![图8-3 Blob的获取和设置](https://github.com/hblvsjtu/JavaScript_Study2.0/blob/master/picture/%E5%9B%BE8-3%20Blob%E7%9A%84%E8%8E%B7%E5%8F%96%E5%92%8C%E8%AE%BE%E7%BD%AE.png?raw=true) 
        
#### 2) Blob的下载
> - 代码，来自[银发Victorique的博客](https://blog.csdn.net/SVictorique/article/details/54892701)
                
                //创建XMLHttpRequest对象
                var xhr = new XMLHttpRequest();
                //配置请求方式、请求地址以及是否同步
                xhr.open('POST', './play', true);
                //设置请求结果类型为blob
                xhr.responseType = 'blob';
                //请求成功回调函数
                xhr.onload = function(e) {
                    if (this.status == 200) {//请求成功
                        //获取blob对象
                        var blob = this.response;
                        //获取blob对象地址，并把值赋给容器
                        $("#sound").attr("src", URL.createObjectURL(blob));
                    }
                };
                xhr.send();

                <video id="sound" width="200" controls="controls"></video>
#### 3) Blob的构造
> - 使用BlobBuilder类
> - Blob.slice() 此方法返回一个新的Blob对象，包含了原Blob对象中指定范围内的数据，出自[hhhyaaon的博客](https://www.cnblogs.com/hhhyaaon/p/5928152.html)
        
                Blob.slice(start:number, end:number, contentType:string)
                start：开始索引，默认为0
                end：截取结束索引（不包括end）
                contentType：新Blob的MIME类型，默认为空字符串
> - 例子
        
                var bb = new BlobBuilder();
                bb.append("This blob contains this text and 10 big-endian 32-bit signed ints");
                bb.append("\0"); //NUL结束符表示字符串的结束

                var ab = new ArrayBuffer(4*10);
                var dv = new DataView(ab);
                for(var i = 0; i < 10; i++) dv.setInt32(i*4,i);
                bb.append(ab);

                //从BlobBuilder中获取blob，并设置类型
                var blob = bb.getBlob("x-optional/mime-type-here");
                var subbb = blob.slice(0, 1024, "text-plain");  //Blob前1kb视为文本
                var last = blob.slice(blob.size-1024, 1024);  //Blob最后1kb视为无类型
                var type = blob.type    //获取blob的MIME类型

#### 4) Blob URL 出自[草根程序猿的博客](https://www.cnblogs.com/jscode/archive/2013/04/27/3572239.html)
> - URL对象用于生成指向File对象或Blob对象的URL。 
        
                var objecturl =  window.URL.createObjectURL(blob);
> - 上面的代码会对二进制数据生成一个URL，类似于“blob:http%3A//test.com/666e6730-f45c-47c1-8012-ccc706f17191”。这个URL可以放置于任何通常可以放置URL的地方，比如img标签的src属性。需要注意的是，即使是同样的二进制数据，每调用一次URL.createObjectURL方法，就会得到一个不一样的URL。
> - 这个URL的存在时间，等同于网页的存在时间，一旦网页刷新或卸载，这个URL就失效。除此之外，也可以手动调用URL.revokeObjectURL方法，使URL失效。
        
                window.URL.revokeObjectURL(objectURL);
> - 下面是一个利用URL对象，在网页插入图片的例子。
        
                var img = document.createElement("img");
                img.src = window.URL.createObjectURL(files[0]);
                img.height = 60;
                img.onload = function(e) {
                    window.URL.revokeObjectURL(this.src);
                }
                body.appendChild(img);
                var info = document.createElement("span");
                info.innerHTML = files[i].name + ": " + files[i].size + " bytes";
                body.appendChild(info);

#### 5) Blob的读取 出自[草根程序猿的博客](https://www.cnblogs.com/jscode/archive/2013/04/27/3572239.html)
> - FileReader对象接收File对象或Blob对象作为参数，用于读取文件的实际内容，即把文件内容读入内存。对于不同类型的文件，FileReader使用不同的方法读取。
> - FileReader.readAsBinaryString(Blob|File) ：读取结果为二进制字符串，每个字节包含一个0到255之间的整数。
> - FileReader.readAsText(Blob|File, opt_encoding) ：读取结果是一个文本字符串。默认情况下，文本编码格式是'UTF-8'，可以通过可选的格式参数，指定其他编码格式的文本。
FileReader.readAsDataURL(Blob|File) ： 读取结果是一个基于Base64编码的 data-uri 对象。
> - FileReader.readAsArrayBuffer(Blob|File) ：读取结果是一个 ArrayBuffer 对象。
> - FileReader采用异步方式读取文件，可以为一系列事件指定回调函数。
>> - onabort：读取中断或调用reader.abort()方法时触发。
>> - onerror：读取出错时触发。
>> - onload：读取成功后触发。
>> - onloadend：读取完成后触发，不管是否成功。触发顺序排在 onload 或 onerror 后面。
>> - onloadstart：读取将要开始时触发。
>> - onprogress：读取过程中周期性触发。
        
<h3 id='8.7'>8.7 文件系统API</h3>    
        
#### 1) 简介 出自[salonzhou的专栏](https://blog.csdn.net/salonzhou/article/details/28275713)
> - “我们不再需要下载并且安装软件。一个简单的web浏览器和一个可供使用的互联网就足以让我们在任何时间，任何地点，还有任何平台上使用任何web应用程序。”简单来说，web应用很酷，但是相对于桌面应用来说，它们有比较显著的弱点：它们无法在一个有层次的文件夹结构体即文件系统中互动和组织。 幸运的是，如果我们使用Filesystem API，我们可以做到。这个API帮助我们控制私有的本地文件系统“沙箱(sandbox)"，在这里我们可以读和写文件，创建和排列文件夹。虽然在我们写这篇文章的时候，只有Google的Chrome完整的支持Filesystem API，我觉得我们还是有必要学习这个强大并且方便的 本地存储特性。
> - 由于并不是非常兼容，这里就不过多叙述

<h3 id='8.8'>8.8 客户端数据库 具体看<a href="https://blog.csdn.net/u013084331/article/details/51336379">u013084331的博客</a></h3>    
        
#### 1) 简述
> - 在HTML5本地存储——Web SQL Database提到过Web SQL Database实际上已经被废弃（由于至今Firefox和IE不支持），而HTML5的支持的本地存储实际上变成了Web Storage（Local Storage和Session Storage）与IndexedDB。Web Storage使用简单字符串键值对在本地存储数据，方便灵活，但是对于大量结构化数据存储力不从心，IndexedDB是为了能够在客户端存储大量的结构化数据，并且使用索引高效检索的API。
#### 2) 基本特性
> - IndexedDB是对象数据库,即NoSQL(Not Only SQL)
> - IndexedDB数据库同样受同源政策的限制(即跨域问题)
> - IndexedDB的每个源都可以有任意数目的IndexedDB数据库。但是每个数据库的名字在该源下必须是唯一的，在IndexDB API中，一个数据库其实就是一个命名的对象存储区间(Object store)的集合。
> - 关系型数据库遵循ACID规则
>> - A (Atomicity) 原子性,事务里的所有操作要么全部做完，要么都不做，事务成功的条件是事务里的所有操作都成功，只要有一个操作失败，整个事务就失败，需要回滚。
>> - C (Consistency) 一致性 数据库要一直处于一致的状态，事务的运行不会改变数据库原本的一致性约束。例如现有完整性约束a+b=10，如果一个事务改变了a，那么必须得改变b，使得事务结束后依然满足a+b=10，否则事务失败。
>> - I (Isolation) 独立性，并发的事务之间不会互相影响，如果一个事务要访问的数据正在被另外一个事务修改，只要另外一个事务未提交，它所访问的数据就不受未提交事务的影响。
>> - D (Durability) 持久性，指一旦事务提交后，它所做的修改将会永久的保存在数据库上，即使出现宕机也不会丢失。
> - 异步API使用   
#### 3) 基本API
> - open() indexedDB.open()方法还有第二个可选参数，数据库版本号，数据库创建的时候默认版本号为1，当我们传入的版本号和数据库当前版本号不一致的时候onupgradeneeded就会被调用，当然我们不能试图打开比当前数据库版本低的version，否则调用的就是onerror了
> - onerror 请求失败的回调函数句柄
> - onsuccess:请求成功的回调函数句柄
> - onupgradeneeded:请求数据库版本变化句柄
> -  关闭数据库可以直接调用数据库对象的close方法;
> -  删除数据库使用indexedDB对象的deleteDatabase方法: 
        
                function openDB (name,version) {  
                    var version=version || 1;  
                    var request=window.indexedDB.open(name,version);  
                    request.onerror=function(e){  
                        console.log(e.currentTarget.error.message);  
                    };  
                    request.onsuccess=function(e){  
                        myDB.db=e.target.result;  
                    };  
                    request.onupgradeneeded=function(e){  
                        console.log('DB version changed to '+version);  
                    };  
                }  
          
                var myDB={  
                    name:'test',  
                    version:3,  
                    db:null  
                };  
                openDB(myDB.name,myDB.version);  
#### 4) object store
> - 有了数据库后我们自然希望创建一个表用来存储数据，但indexedDB中没有表的概念，而是objectStore，一个数据库中可以包含多个objectStore，objectStore是一个灵活的数据结构，可以存放多种类型数据。也就是说一个objectStore相当于一张表，里面存储的每条数据和一个键相关联。
> -  我们可以使用每条记录中的某个指定字段作为键值（keyPath），也可以使用自动生成的递增数字作为键值（keyGenerator），也可以不指定。  
> -  具体的关于数据库的操作我们留到后端二轮的时候来讲； 
        
<h3 id='8.9'>8.9 Web套接字</h3>    
        
#### 1) 简介
> - 让不信任的客户端访问底层的TCP套接字是不安全的，但是WebSocket API定义了一种安全方案，它允许客户端代码在客户端和支持和支持WebSocket协议的服务器端创建双向的套接字类型的连接
> - WebSocket API最伟大之处在于服务器和客户端可以在给定的时间范围内的任意时刻，相互推送信息。WebSocket并不限于以Ajax(或XHR)方式通信，因为Ajax技术需要客户端发起请求，而WebSocket服务器和客户端可以彼此相互推送信息；XHR受到域的限制，而WebSocket允许跨域通信。——来自[晓峰的博客](https://www.cnblogs.com/wei2yi/archive/2011/03/23/1992830.html)
#### 2) 基本API
> - WebSocket()构造函数的参数是一个URL，该URL使用的是ws://协议(或者类似于https://用于安全的wss://协议)
        
                var socket = new WebSocket("ws://hblvsjtu.picp.io:51688/BaiduHomePag.html")
> - socket.onopen =function(e) {/\*套接字已经连接\*/}
> - socket.onclose =function(e) {/\*套接字已经关闭\*/}
> - socket.onerror =function(e) {/\*出错了\*/}
> - socket.onmessage =function(e) { var message = e.data}
> - socket.send("Hello, server!");
> - 代码摘自例22-16
        
            <script>
                window.onload = function() {
                    // Take care of some UI details
                    var nick = prompt("Enter your nickname");     // Get user's nickname
                    var input = document.getElementById("input"); // Find the input field
                    input.focus();                                // Set keyboard focus

                    // Open a WebSocket to send and receive chat messages on.
                    // Assume that the HTTP server we were downloaded from also functions as
                    // a websocket server, and use the same host name and port, but change
                    // from the http:// protocol to ws://
                    var socket = new WebSocket("ws://" + location.host + "/");

                    // This is how we receive messages from the server through the web socket
                    socket.onmessage = function(event) {          // When a new message arrives
                        var msg = event.data;                     // Get text from event object
                        var node = document.createTextNode(msg);  // Make it into a text node
                        var div = document.createElement("div");  // Create a <div>
                        div.appendChild(node);                    // Add text node to div
                        document.body.insertBefore(div, input);   // And add div before input
                        input.scrollIntoView();                   // Ensure input elt is visible
                    }

                    // This is how we send messages to the server through the web socket
                    input.onchange = function() {                 // When user strikes return
                        var msg = nick + ": " + input.value;      // Username plus user's input
                        socket.send(msg);                         // Send it through the socket
                        input.value = "";                         // Get ready for more input
                    }
                };
            </script>
            <!-- The chat UI is just a single, wide text input field -->
            <!-- New chat messages will be inserted before this element -->
            <input id="input" style="width:100%"/>
     
------      
                  
<h2 id='10'> 附件 </h2> 
<h3 id='10.1'>1、遍历样式表结果</h3>
        

        //结果
        body: {background: pink;}
        body: {background: yellow;}
        .top: {padding-right: 95px; min-width: 1000px; height: 30px; font-family: sans-serif; font-size: 12px; line-height: 0px; border-bottom: 1px solid rgb(231, 231, 231);}
        .top a: {padding: 0px 0.5em; line-height: 30px; vertical-align: middle; color: black;}
        .weatherclick: {display: inline-block; margin-left: 15px; padding-right: 7px; text-decoration: none; line-height: 20px !important;}
        .weatherclick:hover: {background: pink;}
        .icon: {display: inline-block; width: 20px; height: 20px; vertical-align: bottom; background: url("https://ss0.bdstatic.com/k4oZeXSm1A5BphGlnYG/icon/weather/aladdin/png_18/a0.png") no-repeat;}
        .weatherquality: {color: rgb(186, 220, 0); margin-left: 7px; margin-right: 7px;}
        .weatherqualitynumber::after: {content: ""; font-size: 10px; border-right: 1px solid black; padding-left: 1em;}
        .toprightlist: {float: right; height: 30px; line-height: 30px; text-align: center; overflow: hidden;}
        .toprightlist:hover: {overflow: visible;}
        .triangle: {width: 0px; border-bottom: 8px solid rgb(153, 153, 153); border-left: 4px solid transparent; border-right: 4px solid transparent; margin-left: auto; margin-right: auto;}
        .outertriangle: {width: 0px; border-bottom: 8px solid rgb(153, 153, 153); border-left: 8px solid transparent; border-right: 8px solid transparent; margin-left: auto; margin-right: auto;}
        .innertriangle: {position: relative; margin-top: -7px; margin-left: auto; margin-right: auto; width: 0px; border-bottom: 7px solid white; border-left: 7px solid transparent; border-right: 7px solid transparent;}
        .toprightlist .itembox: {display: inline-block; margin-top: -1px; line-height: 30px; text-decoration: none; border: 1px solid rgb(153, 153, 153); box-shadow: rgb(153, 153, 153) 2px 2px 2px;}
        .toprightlist li: {display: block; text-align: center;}
        .toprightlist li a: {text-decoration: none;}
        .toprightlink: {float: right; font-size: 14px; line-height: 30px;}
        .productbox: {position: absolute; top: 0px; right: 0px; height: 30px; width: 85px; color: white; background: rgb(57, 139, 251); overflow: hidden;}
        .productbox:hover: {float: none; bottom: 0px; height: 100%; color: black; background: rgb(240, 240, 240);}
        .productupbox: {width: 100%; height: 31px; line-height: 30px; text-align: center;}
        .productupbox span: {font-size: 13px; vertical-align: middle;}
        .productdownbox: {height: 100%; background: rgb(240, 240, 240); overflow: auto;}
        .productdownboxcontent: {height: 700px; width: 65px; margin-left: 10px; background: rgb(240, 240, 240);}
        .productdownboxcontent a: {display: block; padding: 10px 0px; font-size: 12px; color: black; text-align: center; text-decoration: none; border-bottom: 1px solid rgb(231, 231, 231);}
        .productdownboxcontent a:first-child: {margin-top: 10px; border-top: 1px solid rgb(231, 231, 231);}
        .logozone: {margin: 70px auto auto; height: 151px; line-height: 151px; width: 641px; text-align: center;}
        .logozone img: {width: 270px; height: 129px; vertical-align: middle;}
        .searchform: {position: relative; margin: 0px auto; width: 641px; height: 40px; font-size: 0px; text-align: left;}
        .searchinput: {width: 523px; height: 20px; padding: 9px 7px; font-size: 16px; vertical-align: top; border: 1px solid rgb(184, 184, 184);}
        .searchicon: {position: absolute; top: 0px; right: 111px; bottom: 0px; margin: auto; height: 16px; width: 18px; background: -webkit-image-set(url("https://ss1.bdstatic.com/5eN1bjq8AAUYm2zgoY3K/r/www/cache/static/protocol/https/soutu/img/camera_new_5606e8f.png") 1x, url("https://ss1.bdstatic.com/5eN1bjq8AAUYm2zgoY3K/r/www/cache/static/protocol/https/soutu/img/camera_new_x2_fb6c085.png") 2x) no-repeat rgb(255, 255, 255); cursor: pointer;}
        .searchbutton: {display: inline-block; cursor: pointer; margin: 0px; padding: 0px; width: 102px; height: 40px; font-size: 16px; vertical-align: top; color: white; background-color: rgb(51, 136, 255); border: 0px;}
        .contentbox: {margin: 100px auto auto; width: 896px; height: 404px; overflow: hidden; border: 1px solid rgb(231, 231, 231);}
        .contentboxtopbar: {height: 40px; font-size: 0px; line-height: 0; border-bottom: 1px solid rgb(231, 231, 231);}
        .myfocus, .myrecommand, .mynavigation: {display: inline-block; zoom: 1; width: 80px; height: 40px; font-size: 14px; line-height: 40px; color: rgb(51, 51, 51); vertical-align: top; text-align: center; cursor: pointer;}
        .myfocus: {width: 124px;}
        .myrecommand: {color: white; background: rgb(157, 157, 157);}
        .myfocuslogo: {width: 17px; height: 17px; background: url("picture/myfocus_a2.png") 1px 0px no-repeat;}
        .myfocus > *, .myrecommand > *, .mynavigation > *: {vertical-align: middle;}
        .myfocus:hover, .myrecommand:hover, .mynavigation:hover: {font-weight: bold; color: white; background: rgb(190, 190, 190);}
        .contentfocusbox: {display: inline-block; margin-top: 20px; margin-right: 5px; width: 100%;}
        .contentfocusbox aside: {float: right; display: inline-block; width: 300px;}
        .title-text, .hot-refresh, .hot-refresh-text: {color: black; text-decoration: none;}
        .title-text: {font-size: 14px; font-weight: bold;}
        .hot-refresh: {display: block; float: right; height: 22px; padding-top: 3px; padding-right: 30px; width: 60px; cursor: pointer;}
        .hot-refresh-icon: {width: 20px; height: 16px; background: url("https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/mantpl/img/news/news_88aeb6fe.png") -23px -25px no-repeat; vertical-align: bottom;}
        .hot-refresh-text: {font-size: 13px; width: 40px; text-align: center; white-space: nowrap;}
        .newslistul: {float: left; padding-top: 20px; padding-right: 5px; width: 300px;}
        .newslistli: {float: left; display: inline-block; margin-right: 3px; zoom: 1; width: 145px; height: 34px;}
        .newslistli > *: {vertical-align: middle;}
        .newslistli a: {max-width: 113px; font-size: 14px; color: rgb(51, 51, 51); text-overflow: ellipsis; text-decoration: none;}
        .newslistli a:hover: {color: rgb(51, 153, 204); text-decoration: underline; font-weight: bold;}
        .contentfocusboxleftside: {padding: 0px 25px; height: 100px; font-size: 0px;}
        .contentfocusboxleftsidetop: {font-size: 13px; color: rgba(0, 0, 0, 0.4);}
        .contentfocusboxleftsidetop > *: {vertical-align: middle;}
        .line: {display: inline-block; height: 0px; width: 172px; font-size: 0px; border-bottom: 1px solid rgb(226, 226, 226);}
        .baiduicon: {margin: 0px 6px; height: 14px; width: 14px; background: url("picture/zhuazi2.png") 1px 0px no-repeat;}
        .newstable: {float: left; text-align: left; width: 535px;}
        .hot-point: {padding: 0px 2px; font-size: 12px; line-height: 12px; color: rgb(241, 63, 64); border: 1px solid rgb(239, 185, 185); border-radius: 3px;}
        .newsrows1title, .newsrows2title: {width: 100%; font-family: arial, "Microsoft Yahei", 微软雅黑; font-size: 18px; color: rgb(51, 51, 51); font-weight: bold; line-height: 53.6px; vertical-align: middle; text-decoration: none; text-overflow: ellipsis;}
        .newsrows2title: {line-height: 24px;}
        .newsrows1, .newsrows2: {padding-top: 8px; border-bottom: 1px solid rgb(226, 226, 226);}
        .newsrows1picture: {font-size: 3px;}
        .newsrows1 footer, .newsrows2 footer: {padding-top: 10px; padding-bottom: 19px; height: 15px; line-height: 15px; font-size: 13px; color: rgba(0, 0, 0, 0.4);}
        .newsrows1 footer img, .newsrows2 footer img: {float: right; width: 19px; height: 15px; background: url("https://ss0.bdstatic.com/5aV1bjqh_Q23odCf/static/mantpl/img/news/dustbin_new_41cbcb37.png") 0px -19px no-repeat; visibility: hidden;}
        .src-net, .src-time: {margin-right: 10px; line-height: 15px; font-size: 13px; text-decoration: none; color: rgba(0, 0, 0, 0.4);}
        .newsrows2: {display: table; zoom: 1; min-height: 140px; overflow: hidden;}
        .newsrows2picture: {display: table-cell; padding: 20px 0px; vertical-align: middle; zoom: 1;}
        .newsrows2textzone: {display: table-cell; padding-left: 21px; zoom: 1; width: 337px; vertical-align: middle;}
        .morebar: {padding-top: 20px; margin: auto; cursor: pointer; width: 90px; height: 45px; text-align: center;}
        .morebartext: {font-size: 12px; color: rgb(153, 153, 153);}
        .morebartexttriangele: {height: 18px; width: 34px; margin: 10px auto 0px; border: 0px; font-size: 0px;}
        .morebaroutertriangele: {position: relative; margin: 0px; padding: 0px; width: 0px; border-width: 16px; border-style: solid; border-color: black transparent transparent; border-image: initial;}
        .morebarinnertriangele: {position: absolute; top: -16px; left: -15px; margin: 0px; padding: 0px; width: 0px; border-width: 15px; border-style: solid; border-color: white transparent transparent; border-image: initial;}
        .myfooter: {margin: 70px auto; color: rgb(153, 153, 153); zoom: 1; font-size: 12px; text-align: center;}
        .myfooter *: {vertical-align: middle; color: rgb(153, 153, 153); line-height: 19px;}
        .ICPlogo: {display: inline-block; width: 19px; height: 19px; background: url("picture/ICPlogo2.png") 3px 0px no-repeat rgb(255, 255, 255);}
        .sercuelogo: {display: inline-block; width: 20px; height: 20px; background: url("picture/surcue2.png") 3px 0px no-repeat rgb(255, 255, 255);}

       
<h3 id='10.2'>2、HTTP状态码列表</h3>        
        
<center>**[HTTP状态码列表](http://www.runoob.com/http/http-status-codes.html)**</center>
>> 状态码 | 状态码英文名称 | 中文描述
>> -|-|-
>> 100 | Continue | 继续。客户端应继续其请求
>> 101 | Switching Protocols | 切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议
>> 200 | OK | 请求成功。一般用于GET与POST请求
>> 201 | Created | 已创建。成功请求并创建了新的资源
>> 202 | Accepted | 已接受。已经接受请求，但未处理完成
>> 203 | Non-Authoritative Information | 非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本
>> 204 | No Content | 无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档
>> 205 | Reset Content | 重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域
>> 206 | Partial Content | 部分内容。服务器成功处理了部分GET请求
>> 300 | Multiple Choices | 多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择
>> 301 | Moved Permanently | 永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替
>> 302 | Found | 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
>> 303 | See Other | 查看其它地址。与301类似。使用GET和POST请求查看
>> 304 | Not Modified | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
>> 305 | Use Proxy | 使用代理。所请求的资源必须通过代理访问
>> 306 | Unused | 已经被废弃的HTTP状态码
>> 307 | Temporary Redirect | 临时重定向。与302类似。使用GET请求重定向
>> 400 | Bad Request | 客户端请求的语法错误，服务器无法理解
>> 401 | Unauthorized | 请求要求用户的身份认证
>> 402 | Payment Required | 保留，将来使用
>> 403 | Forbidden | 服务器理解请求客户端的请求，但是拒绝执行此请求
>> 404 | Not Found | 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面
>> 405 | Method Not Allowed | 客户端请求中的方法被禁止
>> 406 | Not Acceptable | 服务器无法根据客户端请求的内容特性完成请求
>> 407 | Proxy Authentication Required | 请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权
>> 408 | Request Time-out | 服务器等待客户端发送的请求时间过长，超时
>> 409 | Conflict |  服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突
>> 410 | Gone | 客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置
>> 411 | Length Required | 服务器无法处理客户端发送的不带Content-Length的请求信息
>> 412 | Precondition Failed | 客户端请求信息的先决条件错误
>> 413 | Request Entity Too Large | 由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息
>> 414 | Request-URI Too Large | 请求的URI过长（URI通常为网址），服务器无法处理
>> 415 | Unsupported Media Type | 服务器无法处理请求附带的媒体格式
>> 416 | Requested range not satisfiable | 客户端请求的范围无效
>> 417 | Expectation Failed | 服务器无法满足Expect的请求头信息
>> 500 | Internal Server Error | 服务器内部错误，无法完成请求
>> 501 | Not Implemented | 服务器不支持请求的功能，无法完成请求
>> 502 | Bad Gateway | 充当网关或代理的服务器，从远端服务器接收到了一个无效的请求
>> 503 | Service Unavailable | 由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中
>> 504 | Gateway Time-out | 充当网关或代理的服务器，未及时从远端服务器获取请求
>> 505 | HTTP Version not supported | 服务器不支持请求的HTTP协议的版本，无法完成处理

<h3 id='10.3'>3、permanote.js</h3>   
        
                // Some variables we need throughout
                var editor, statusline, savebutton, idletimer;

                // The first time the application loads
                window.onload = function() {
                    // Initialize local storage if this is the first time
                    if (localStorage.note == null) localStorage.note = "";
                    if (localStorage.lastModified == null) localStorage.lastModified = 0;
                    if (localStorage.lastSaved == null) localStorage.lastSaved = 0;

                    // Find the elements that are the editor UI. Initialize global variables.
                    editor = document.getElementById("editor");
                    statusline = document.getElementById("statusline");
                    savebutton = document.getElementById("savebutton");

                    editor.value = localStorage.note; // Initialize editor with saved note
                    editor.disabled = true;           // But don't allow editing until we sync

                    // Whenever there is input in the textarea
                    editor.addEventListener("input",
                                            function (e) {
                                                // Save the new value in localStorage
                                                localStorage.note = editor.value;
                                                localStorage.lastModified = Date.now();
                                                // Reset the idle timer
                                                if (idletimer) clearTimeout(idletimer);
                                                idletimer = setTimeout(save, 5000);
                                                // Enable the save button
                                                savebutton.disabled = false;
                                            },
                                            false);

                    // Each time the application loads, try to sync up with the server
                    sync();
                };

                // Save to the server before navigating away from the page
                window.onbeforeunload = function() {
                    if (localStorage.lastModified > localStorage.lastSaved)
                        save();
                };

                // If we go offline, let the user know
                window.onoffline = function() { status("Offline"); }

                // When we come online again, sync up.
                window.ononline = function() { sync(); };

                // Notify the user if there is a new version of this application available.
                // We could also force a reload here with location.reload()
                window.applicationCache.onupdateready = function() {
                    status("A new version of this application is available. Reload to run it");
                };

                // Also let the user know if there is not a new version available.
                window.applicationCache.onnoupdate = function() {
                    status("You are running the latest version of the application.");
                };

                // A function to display a status message in the status line
                function status(msg) { statusline.innerHTML = msg; }

                // Upload the note text to the server (if we're online).
                // Will be automatically called after 5 seconds of inactivity whenever
                // the note has been modified.
                function save() {
                    if (idletimer) clearTimeout(idletimer);
                    idletimer = null;

                    if (navigator.onLine) {
                        var xhr = new XMLHttpRequest();
                        xhr.open("PUT", "/note");
                        xhr.send(editor.value);
                        xhr.onload = function() {
                            localStorage.lastSaved = Date.now();
                            savebutton.disabled = true;
                        };
                    }
                }

                // Check for a new version of the note on the server. If a newer
                // version is not found, save the current version to the server.
                function sync() {
                   if (navigator.onLine) {
                        var xhr = new XMLHttpRequest();
                        xhr.open("GET", "/note");
                        xhr.send();
                        xhr.onload = function() {
                            var remoteModTime = 0;
                            if (xhr.status == 200) {
                                var remoteModTime = xhr.getResponseHeader("Last-Modified");
                                remoteModTime = new Date(remoteModTime).getTime();
                            }

                            if (remoteModTime > localStorage.lastModified) {
                                status("Newer note found on server.");
                                var useit =
                                    confirm("There is a newer version of the note\n" +
                                            "on the server. Click Ok to use that version\n"+
                                            "or click Cancel to continue editing this\n"+
                                            "version and overwrite the server");
                                var now = Date.now();
                                if (useit) {
                                    editor.value = localStorage.note = xhr.responseText;
                                    localStorage.lastSaved = now;
                                    status("Newest version downloaded.");
                                }
                                else 
                                    status("Ignoring newer version of the note.");
                                localStorage.lastModified = now;
                            }
                            else
                                status("You are editing the current version of the note.");

                            if (localStorage.lastModified > localStorage.lastSaved) {
                                save();
                            }

                            editor.disabled = false;  // Re-enable the editor
                            editor.focus();           // And put cursor in it
                        }
                    }
                    else { // If we are currently offline, we can't sync
                        status("Can't sync while offline");
                        editor.disabled = false;
                        editor.focus();
                    }
                }       









