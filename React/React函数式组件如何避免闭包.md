# React函数式组件如何避免闭包

通过简化状态重用和副作用管理，Hooks 取代了基于类的组件。此外，咱们可以将重复的逻辑提取到自定义 Hook 中，以便在应用程序之间重用。

Hooks 严重依赖于 JS 闭包,但是闭包有时很棘手。

1. 正确管理hook依赖关系解决hook闭包的关键，推荐安装 eslint-plugin-react-hooks,它可以帮助咱们检测被遗忘的依赖项
2. useState定义的setState方法，在使用时把参数值改为方法，比如：把`setStateValue('Hello World')` 改为 `setStateValue(() => 'Hello World')`
