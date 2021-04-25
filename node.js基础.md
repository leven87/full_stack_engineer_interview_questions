### Node.js 基础
---
#### Node.js 框架
* Apollo Server. it is a flexible, community driven, production-ready HTTP GraphQL middleware for Express, Hapi, Koa, and more. 仔细查看apollo server 的代码，可以看到
```
import express from 'express';
```
说明它是内置有express框架的。

* Express Express是一个最小且灵活的Web应用程序框架，为Web和移动应用程序提供了一组强大的功能，它的行为就像一个中间件，可以帮助管理服务器和路由。
  * 缺点
    * 组织需要非常清楚，代码维护困难
    * 随着代码库大小的增加，重构变得非常具有挑战性 
    * 需要大量的手工劳动，因为您需要创建所有端点   
  * 优点
    * 小巧，简单，灵活
    * 快速开发
    * 可定制
 * Koa Koa 是一个新的 web 框架，由 Express幕后的原班人马打造，致力于成为web应用和API开发领域中的一个更小、更富有表现力、更健壮的基石。 通过利用 async 函数，Koa帮你丢弃回调函数，并有力地增强错误处理Koa并没有捆绑任何中间件而是提供了一套优雅的方法，帮助您快速而愉快地编写服务端应用程序
   * 优点
     * Koa提高了互操作性，健壮性，使编写中间件变得更加愉快。
     * 集成了大量的web API，但是没有绑定中间件
     * 非常轻量，核心的Koa模块只有大约2K行代码
     * 拥有非常好的用户体验
     * 通过try / catch更好地处理错误
     * 异步控制流，代码可读性更高
     
   * 缺点
     * Koa社区相对较小
     * 与Express风格的中间件不兼容(目前还有遇到与其他框架兼容的中间件)
     
  * Hapi Hapi是基础功能相对丰富的框架。开发人员更专注于业务，而不是花时间构建基础架构。配置驱动的模式，区别于传统的web服务器操作。他还有比一个独特功能，能够在特定的IP上创建服务器，具有类似的功能onPreHandler。需要的时候你可以拦截特地的请求做一些必要的操作。
    * 优点
      * 提供了一个强大的插件系统，允许您快速添加新功能和修复错误
      * 可扩展的API
      * 对请求处理有更深层次的控制。
      * 创建(REST)api的最佳选择，提供了路由、输入、输出验证和缓存
      * 一次编写适配各端
      * 详细的API参考和对文档生成的良好支持
      * 与任何前端框架（如React，Angular和Vue.js）一起使用来创建单页面应用程序
      * 基于配置的伪中间件
      * 提供缓存，身份验证和输入验证
      * 提供基于插件的扩展架构
      * 提供非常好的企业插件，如joi，yar，catbox，boom，tv和travelogue    
       
    * 缺点
      * 代码结构复杂
      * 插件不兼容，只能使用指定的插件如：catbox joi boom tv good travelogue等
      * 端点是手动创建的，必须手动测试
      * 重构是手动的     

#### var, let, const 的区别。
* var 没有块作用域
* let 是更完美的var
  * let声明的变量拥有块级作用域。
  * let声明的全局变量不是全局对象的属性。这就意味着，你不可以通过window.变量名的方式访问这些变量。它们只存在于一个不可见的块的作用域中.
  * 形如for (let x...)的循环在每次迭代时都为x创建新的绑定。
  * 用let重定义变量会抛出一个语法错误（SyntaxError）。如以下是错误的：
  ```
  let a = 'a';
  let a = 'b';
  ```
* const 是用来定义常量的，一旦被定义，它的值是不能改变的。

#### Promise  
它利用then和catch，能让异步代码像同步代码一样优雅的书写。

#### js里边的this指的是什么?  
this指的是对象本身，而不是构造函数．

#### apply, call和bind有什么区别?  
三者都可以把一个函数应用到其他对象上.
```
	function Person() {
	}
	Person.prototype.sayName() { alert(this.name); }

	var obj = {name: 'michaelqin'}; // 注意这是一个普通对象，它不是Person的实例
	1) apply
	Person.prototype.sayName.apply(obj, [param1, param2, param3]);

	2) call
	Person.prototype.sayName.call(obj, param1, param2, param3);

	3) bind
	var sn = Person.prototype.sayName.bind(obj);
	sn([param1, param2, param3]); // bind需要先绑定，再执行
	sn(param1, param2, param3); // bind需要先绑定，再执行
```
使得obj对象有了sayName这个方法。

#### js常用设计模式？  
单例，工厂，代理，装饰，观察者模式等。

####  Html5有哪些比较实用新功能？
* File API支持本地文件操作; 参看：https://www.shangmayuan.com/a/a6a1b71897f44baca0b8622c.html  
  * 实现文件多选
  * 实现文件从计算机拖拽到网页以及添加文件队列功能 
  * 文件续传原理
  * 文件前端切片
  * 文件片断的上传
* Canvans/SVG支持绘图; 拖拽功能支持; 
* 本地存储支持; 
* 表单多属性验证支持; 原生音频视频支持等。
* websocket

#### node.js 的同步和异步怎么理解？  
node是单线程的，异步是通过一次次的循环事件队列来实现的．同步则是说阻塞式的IO,这在高并发环境会是一个很大的性能问题，所以同步一般只在基础框架的启动时使用，用来加载配置文件，初始化程序什么的．

#### 有哪些方法可以进行异步流程的控制?
* 多层嵌套回调 
* 为每一个回调写单独的函数，函数里边再回调 
* 用第三方框架比方async, q, promise等
#### 怎样调节node执行单元的内存大小?   
用--max-old-space-size 和 --max-new-space-size 来设置 v8 使用内存的上限。

#### async都有哪些常用方法，分别是怎么用?
* async.parallel并行执行完多个函数后，调用结束函数
* async.series串行执行完多个函数后，调用结束函数
* async.waterfall依次执行多个函数，后一个函数以前面函数的结果作为输入参数
* async.map异步执行多个数组，返回结果数组
* async.filter异步过滤多个数组，返回结果数组

#### 列举数组相关的常用方法?  
push/pop, shift/unshift, split/join, slice/splice/concat, sort/reverse, map/reduce, forEach, filter

#### 列举字符串相关的常用方法?  
indexOf/lastIndexOf/charAt, split/match/test, slice/substring/substr, toLowerCase/toUpperCase

#### node的构架是什么样子的?  
主要分为三层，应用app >> V8及node内置架构 >> 操作系统. V8是node运行的环境，可以理解为node虚拟机．
node内置架构又可分为三层: 核心模块(javascript实现) >> c++绑定 >> libuv + CAes + http.

#### node中的Buffer如何应用?  
Buffer是用来处理二进制数据的，比如图片，mp3,数据库文件等.Buffer支持各种编码解码，二进制字符串互转．

#### 什么是EventEmitter?  
EventEmitter是node中一个实现观察者模式的类，主要功能是监听和发射消息，用于处理多模块交互问题.

#### EventEmitter有哪些典型应用?  
* 模块间传递消息 
* 回调函数内外传递消息 
* 处理流数据，因为流是在EventEmitter基础上实现的.
* 观察者模式发射触发机制相关应用

#### 怎么捕获EventEmitter的错误事件?  
监听error事件即可．如果有多个EventEmitter,也可以用domain来统一处理错误事件.


#### EventEmitter中的newListenser事件有什么用处?  
newListener可以用来做事件机制的反射，特殊应用，事件管理等．当任何on事件添加到EventEmitter时，就会触发newListener事件，基于这种模式，我们可以做很多自定义处理.

#### 内置的fs模块架构是什么样子的?  
fs模块主要由下面几部分组成: 
* 1) POSIX文件Wrapper,对应于操作系统的原生文件操作 
* 2) 文件流 fs.createReadStream和fs.createWriteStream 
* 3) 同步文件读写,fs.readFileSync和fs.writeFileSync 
* 4) 异步文件读写, fs.readFile和fs.writeFile

#### 怎么读取json配置文件?
* 第一种是利用node内置的require('data.json')机制，直接得到js对象; 
* 第二种是读入文件入内容，然后用JSON.parse(content)转换成js对象．  
区别：二者的区别是require机制情况下，如果多个模块都加载了同一个json文件，那么其中一个改变了js对象，其它跟着改变，这是由node模块的缓存机制造成的，只有一个js模块对象; 第二种方式则可以随意改变加载后的js变量，而且各模块互不影响，因为他们都是独立的，是多个js对象。  

#### node.js的网络模块架构是什么样子的?  
node全面支持各种网络服务器和客户端，包括tcp, http/https, tcp, udp, dns, tls/ssl等. 

#### 实现一个简单的http服务器？  
加载http模块，创建服务器，监听端口.


#### 为什么需要child-process?  
node是异步非阻塞的，这对高并发非常有效．可是我们还有其它一些常用需求，比如和操作系统shell命令交互，调用可执行文件，创建子进程进行阻塞式访问或高CPU计算等，child-process就是为满足这些需求而生的．child-process顾名思义，就是把node阻塞的工作交给子进程去做．

#### 两个node程序之间怎样交互?
* 用fork, 原理是子程序用process.on, process.send，
* 父程序里用child.on,child.send进行交互.

#### 怎样让一个js文件变得像linux命令一样可执行?
* 1) 在myCommand.js文件头部加入 #!/usr/bin/env node 
* 2) chmod命令把js文件改为可执行即可 
* 3) 进入文件目录，命令行输入myComand 就是相当于node myComand.js了





