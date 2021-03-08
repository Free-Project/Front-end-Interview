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
### 5、TCP的3次握手
### 6、TCP属于哪一层（1 物理层 -> 2 数据链路层 -> 3 网络层(ip)-> 4 传输层(tcp) -> 5 应用层(http)）
### 7、前端开发中用到哪些设计模式
### 8、介绍下数字签名的原理
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
1. 对PWA有什么了解
2. RESTful常用的Method
3. base64为什么能提升性能，缺点
4. 介绍webp这个图片文件格式
5. 介绍DNS解析
6. 介绍SSL和TLS
7. 介绍异步方案
8. 对无状态组件的理解
9、介绍快速排序
10. 介绍下DFS深度优先

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
