# 前端面试题-通信/编程/原理篇

## 一、原理篇

### 1、介绍观察者模式
观察者模式又称发布订阅模式（Publish/Subscribe Pattern），是我们经常接触到的设计模式，日常生活中的应用也比比皆是，比如你订阅了某个博主的频道，当有内容更新时会收到推送；又比如JavaScript中的事件订阅响应机制。观察者模式的思想用一句话描述就是：被观察对象（subject）维护一组观察者（observer），当被观察对象状态改变时，通过调用观察者的某个方法将这些变化通知到观察者。  

比如给DOM元素绑定事件的 `addEventListener()` 方法：
```
target.addEventListener(type, listener [, options]);
```
Target就是被观察对象Subject，listener就是观察者Observer。   

观察者模式中Subject对象一般需要实现以下API：

- subscribe(): 接收一个观察者observer对象，使其订阅自己
- unsubscribe(): 接收一个观察者observer对象，使其取消订阅自己
- fire(): 触发事件，通知到所有观察者

用JavaScript手动实现观察者模式：  
```
// 被观察者
function Subject() {
  this.observers = [];
}

Subject.prototype = {
  // 订阅
  subscribe: function (observer) {
    this.observers.push(observer);
  },
  // 取消订阅
  unsubscribe: function (observerToRemove) {
    this.observers = this.observers.filter(observer => {
      return observer !== observerToRemove;
    })
  },
  // 事件触发
  fire: function () {
    this.observers.forEach(observer => {
      observer.call();
    });
  }
}
```
验证一下订阅是否成功：
```
const subject = new Subject();

function observer1() {
  console.log('Observer 1 Firing!');
}

function observer2() {
  console.log('Observer 2 Firing!');
}

subject.subscribe(observer1);
subject.subscribe(observer2);
subject.fire();
```
输出：
```
Observer 1 Firing! 
Observer 2 Firing!
```
验证一下取消订阅是否成功：
```
subject.unsubscribe(observer2);
subject.fire();
```
输出：
```
Observer 1 Firing!
```

### 2、介绍中介者模式
在中介者模式中，中介者（Mediator）包装了一系列对象相互作用的方式，使得这些对象不必直接相互作用，而是由中介者协调它们之间的交互，从而使它们可以松散偶合。当某些对象之间的作用发生改变时，不会立即影响其他的一些对象之间的作用，保证这些作用可以彼此独立的变化。  

中介者模式和观察者模式有一定的相似性，都是一对多的关系，也都是集中式通信，不同的是中介者模式是处理同级对象之间的交互，而观察者模式是处理Observer和Subject之间的交互。中介者模式有些像婚恋中介，相亲对象刚开始并不能直接交流，而是要通过中介去筛选匹配再决定谁和谁见面。中介者模式比较常见的应用比如聊天室，聊天室里面的人之间并不能直接对话，而是通过聊天室这一媒介进行转发。一个简易的聊天室模型可以实现如下：

聊天室成员类：  
```
function Member(name) {
  this.name = name;
  this.chatroom = null;
}

Member.prototype = {
  // 发送消息
  send: function (message, toMember) {
    this.chatroom.send(message, this, toMember);
  },
  // 接收消息
  receive: function (message, fromMember) {
    console.log(`${fromMember.name} to ${this.name}: ${message}`);
  }
}
```
聊天室类：
```
function Chatroom() {
  this.members = {};
}

Chatroom.prototype = {
  // 增加成员
  addMember: function (member) {
    this.members[member.name] = member;
    member.chatroom = this;
  },
  // 发送消息
  send: function (message, fromMember, toMember) {
    toMember.receive(message, fromMember);
  }
}
```
测试一下：
```
const chatroom = new Chatroom();
const bruce = new Member('bruce');
const frank = new Member('frank');

chatroom.addMember(bruce);
chatroom.addMember(frank);

bruce.send('Hey frank', frank);
```
输出：
```
bruce to frank: hello frank
```
这只是一个最简单的聊天室模型，真正的聊天室还可以加入更多的功能，比如敏感信息拦截、一对多聊天、广播等。得益于中介者模式，Member不需要处理和聊天相关的复杂逻辑，而是全部交给Chatroom，有效的实现了关注分离。



### 3、观察者和订阅-发布的区别，各自用在哪里
### 4、介绍事件代理以及优缺点
事件委托原理：事件冒泡机制。  
优点：
1. 可以大量节省内存占用，减少事件注册。比如ul上代理所有li的click事件就很不错。
2. 可以实现当新增子对象时，无需再对其进行事件绑定，对于动态内容部分尤为合适

缺点：事件代理的常用应用应该仅限于上述需求，如果把所有事件都用事件代理，可能会出现事件误判。即本不该被触发的事件被绑定上了事件。

### 5、TCP的3次握手
### 6、TCP属于哪一层（1 物理层 -> 2 数据链路层 -> 3 网络层(ip)-> 4 传输层(tcp) -> 5 应用层(http)）
### 7、前端开发中用到哪些设计模式
### 8、介绍下数字签名的原理
数字签名含义是：在网络中传输数据时候，给数据添加一个数字签名，表示是谁发的数据，而且还能证明数据没有被篡改。  
数字签名的主要作用就是保证了数据的有效性（验证是谁发的）和完整性（证明信息没有被篡改）。

### 9、Promise.all实现原理


## 二、算法/编程篇
1. 介绍AST（Abstract Syntax Tree）抽象语法树
2. 柯里化函数两端的参数具体是什么东西
3. 介绍二叉搜索树的特点
4. [1, 2, 3, 4, 5]变成[1, 2, 3, a, b, 5]
5. 如何找0-5的随机数，95-99呢
6. 手写数组扁平化函数
7. 写一个倒计时函数
8. 写一个函数，给定一棵树，输出这棵树的深度
9. 写一个函数，给定一个url和最大深度maxdeep，输出抓取当前url及其子链接深度范围内的所有图片
10. 写一个函数，给定nodes=[]，每一个节点拥有id,name,parentid，输出一个属性列表的展示(涉及dom操作)
11. "123456789876543212345678987654321..."的第n位是什么？

## 三、测试篇
1. 前端怎么做单元测试
2. pm2怎么做进程管理，进程挂掉怎么处理
3. 不用pm2怎么做进程管理

## 四、了解篇
### 1、对PWA的了解
PWA全称Progressive Web App，即渐进式WEB应用。  
一个 PWA 应用首先是一个网页, 可以通过 Web 技术编写出一个网页应用. 随后添加上 App Manifest 和 Service Worker 来实现 PWA 的安装和离线等功能

解决了哪些问题？  

- 可以添加至主屏幕，点击主屏幕图标可以实现启动动画以及隐藏地址栏
- 实现离线缓存功能，即使用户手机没有网络，依然可以使用一些离线功能
- 实现了消息推送

它解决了上述提到的问题，这些特性将使得 Web 应用渐进式接近原生 App。


### 2、对SSR的理解
Server Side Render：服务端渲染  
**概念**  
解释一：服务端在返回 html 之前，在特定的区域，符号里用数据填充，再给客户端，客户端只负责解析 HTML 。  

解释二：服务端渲染的模式下，当用户第一次请求页面时，由服务器把需要的组件或页面渲染成 HTML 字符串，然后把它返回给客户端。客户端拿到手的，是可以直接渲染然后呈现给用户的 HTML 内容，不需要为了生成 DOM 内容自己再去跑一遍 JS 代码。使用服务端渲染的网站，可以说是“所见即所得”，页面上呈现的内容，我们在 html 源文件里也能找到。  

**利弊**  
好处:首屏渲染快、利于SEO、可以生成缓存片段，生成静态化文件、节能（对比客户端渲染的耗电）  
坏处:用户体验较差、不容易维护，通常前端改了部分html或者css，后端也需要修改。  

**对比**  
其实前后端的渲染本质是一样的，都是字符串的拼接，将数据渲染进一些固定格式的html代码中形成最终的html展示在用户页面上。 因为字符串的拼接必然会损耗一些性能资源。  
如果在服务器端渲染，那么消耗的就是server端的性能。  
如果是在客户端渲染，常见的手段，比如是直接生成DOM插入到html 中，或者是使用一些前端的模板引擎等。他们初次渲染的原理大多是将原html中的数据标记（例如{{text}}）替换。  

更多https://www.jianshu.com/p/b8cfa496b7ec

### 3、RESTful常用的Method
http://www.ruanyifeng.com/blog/2011/09/restful.html

### 4、base64为什么能提升性能，缺点
### 5、介绍webp这个图片文件格式
### 6、介绍DNS解析
### 7、介绍SSL和TLS
### 8、介绍异步方案
### 9、对无状态组件的理解
无状态组件不像其他两种方法在调用时会创建新实例，它创建时始终保持了一个实例，避免了不必要的检查和内存分配，做到了内部优化。  
无状态组件不会被实例化，无实例化过程也就不需要分配多余的内存，所以相比有状态组件，它的性能更优。同样，由于没有实例化，所以无法访问组件this中的对象，例如：this.ref、this.state 等均不能访问

### 10、介绍快速排序
### 11、介绍下DFS深度优先

## 五、通信篇
1. ajax如何处理跨域
2. Ajax发生跨域要设置什么（前端）
3. 跨域jsonp方案需要服务端怎么配合
4. Async里面有多个await请求，可以怎么优化（请求是否有依赖）
5. ajax的步骤
6. CORS如何设置
7. jsonp为什么不支持post方法
8. axios有什么特点？

## 六、优化及语义
1. 前端需要注意哪些SEO
2. 如何进行网站性能优化
3. 语义化的理解
4. CSS在性能优化方面的实践
