# React-Hook使用规则

Hooks仅仅是JavaScript方法，但在使用的时候要遵循正确的使用方式。我们提供一个linter插件来自动检查。

### 1、只在最顶层调用Hooks
不要在**循环、条件语句或者嵌套方法**中调用Hooks。要在你React方法的顶层里调用。    
这是因为React需要利用调用顺序来正确更新相应的状态，以及调用相应的Hooks函数。一旦在循环或条件分支语句中调用Hook，就容易导致调用顺序的不一致性，从而产生难以预料到的后果。  

### 2、只能在function组件里调用Hooks
不能在普通JavaScript方法里调用Hooks。

你只能
- 在function组件里调用Hooks
- 在自定义Hooks里调用Hooks

遵循这个能保证所有组件里的有状态逻辑足够清晰。
