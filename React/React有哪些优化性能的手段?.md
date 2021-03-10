# React有哪些优化性能的手段?

## 类组件中的优化手段

- 使用纯组件 PureComponent 作为基类。
- 使用 React.memo 高阶函数包装组件。
- 使用 shouldComponentUpdate 生命周期函数来自定义渲染逻辑。

## 方法组件中的优化手段
- 使用 useMemo。
- 使用 useCallBack。

## 其他方式
- 在列表需要频繁变动时，使用唯一 id 作为 key，而不是数组下标。
- 必要时通过改变 CSS 样式隐藏显示组件，而不是通过条件判断显示隐藏组件。
- 使用 Suspense 和 lazy 进行懒加载，例如：

```
import React, { lazy, Suspense } from "react";

export default class CallingLazyComponents extends React.Component {
  render() {
    var ComponentToLazyLoad = null;

    if (this.props.name == "Mayank") {
      ComponentToLazyLoad = lazy(() => import("./mayankComponent"));
    } else if (this.props.name == "Anshul") {
      ComponentToLazyLoad = lazy(() => import("./anshulComponent"));
    }

    return (
      <div>
        <h1>This is the Base User: {this.state.name}</h1>
        <Suspense fallback={<div>Loading...</div>}>
          <ComponentToLazyLoad />
        </Suspense>
      </div>
    )
  }
}
```
> Suspense 用法可以参考官方文档 https://zh-hans.reactjs.org/docs/concurrent-mode-suspense.html

> 相关阅读： 21个React性能优化技巧 https://www.infoq.cn/article/KVE8xtRs-uPphptq5LUz
