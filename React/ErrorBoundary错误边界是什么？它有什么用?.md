## ErrorBoundary错误边界是什么？它有什么用？
在 React 中，如果任何一个组件发生错误，它将破坏整个组件树，导致整页白屏。这时候我们可以用错误边界优雅地降级处理这些错误。

例如下面封装的组件：
```
class ErrorBoundary extends React.Component<IProps, IState> {
  constructor(props: IProps) {
    super(props);
    this.state = { hasError: false };
  }

  static getDerivedStateFromError() {
    // 更新 state 使下一次渲染能够显示降级后的 UI
    return { hasError: true };
  }

  componentDidCatch(error, errorInfo) {
    // 可以将错误日志上报给服务器
    console.log('组件奔溃 Error', error);
    console.log('组件奔溃 Info', errorInfo);
  }

  render() {
    if (this.state.hasError) {
      // 你可以自定义降级后的 UI 并渲染
      return this.props.content;
    }
    return this.props.children;
  }
}
```
