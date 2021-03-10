# React Fiber 是什么？

React Fiber 是一种基于浏览器的单线程调度算法。

是为了解决 diff 时间过长导致的卡顿问题，React Fiber 用类似 `requestIdleCallback` 的机制来做异步 diff。但是之前的数据结构不支持这样的实现异步 diff，于是 React 实现了一个类似链表的数据结构，将原来的 递归diff 变成了现在的 遍历diff，这样就能方便的做中断和恢复。

### 相关阅读

[react-fiber-architecture](https://github.com/acdlite/react-fiber-architecture)

[理解 React Fiber & Concurrent Mode](https://zhuanlan.zhihu.com/p/109971435)

[The how and why on React’s usage of linked list in Fiber to walk the component’s tree](https://juejin.im/post/6844903753347252237)

[Inside Fiber: in-depth overview of the new reconciliation algorithm in React](https://juejin.im/post/6844903844825006087)
