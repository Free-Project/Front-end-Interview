# React-Hook使用规则

Hooks仅仅是JavaScript方法，但在使用的时候要遵循正确的使用方式。我们提供一个linter插件来自动检查。

### 1 只在最顶层调用Hooks
不要在**循环、条件语句或者嵌套方法**中调用Hooks。要在你React方法的顶层里调用。遵循这个方式，你能保证每次组件渲染时Hooks都是按照相同的顺序被调用。这能使React在多个useState和useEffect的情形下正确保存state数据。

### 2 只能在function组件里调用Hooks
不能在普通JavaScript方法里调用Hooks。

你只能
- 在function组件里调用Hooks
- 在自定义Hooks里调用Hooks

遵循这个能保证所有组件里的有状态逻辑足够清晰。
