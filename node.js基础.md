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

#### Promise 它利用then和catch，能让异步代码像同步代码一样优雅的书写。

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
