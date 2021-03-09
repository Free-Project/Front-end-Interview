# React函数式组件如何避免闭包

通过简化状态重用和副作用管理，Hooks 取代了基于类的组件。此外，咱们可以将重复的逻辑提取到自定义 Hook 中，以便在应用程序之间重用。

Hooks 严重依赖于 JS 闭包,但是闭包有时很棘手。

1. 正确管理hook依赖关系解决hook闭包的关键，推荐安装 eslint-plugin-react-hooks,它可以帮助咱们检测被遗忘的依赖项
2. 通过函数方法来更新`state`状态
示例：
```
function DelayedCount() {
  const [count, setCount] = useState(0);

  function handleClickAsync() {
    setTimeout(function delay() {
      setCount(count + 1); // 闭包产生了
      setCount(count => count + 1); // 改为通过函数方法来更新 count 状态
    }, 1000);
  }

  function handleClickSync() {
    setCount(count + 1);
  }

  return (
    <div>
      {count}
      <button onClick={handleClickAsync}>Increase async</button>
      <button onClick={handleClickSync}>Increase sync</button>
    </div>
  );
}
```
