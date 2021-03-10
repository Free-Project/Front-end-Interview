# React中useEffect(fn, [])和ComponentDidMount的区别
hook和生命周期方法基于完全不同的原理。 诸如componentDidMount()类的方法围绕生命周期和渲染时间展开，而useEffect(fn, [])则围绕状态和与DOM的同步进行设计。
> 类似的问题，为什么有时候在effect里拿到的是旧的state或prop呢？

```
import React, { useState, useEffect } from 'react';

function App() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    setTimeout(() => {
      console.log(count);
    } , 3000)
  }, []);

  return (
    <div className="APP">
      <p>count: {count}</p>
      <button onClick={() => setCount(count + 1)}>
        Click
      </button>
    </div>
  );
}
```
useEffect会捕获props, state，但是始终是初始的值。 如上图所示，当我们点击button多次，effect在3秒之后的回调，打印的依然是count的初始值。

**为什么会这样？**
`这是因为javascript闭包的机制`，函数组件被调用后，函数内部的state由于被内部定时器的回调所依赖，所以没有被垃圾回收机制所清除，而是保存在内存里了。所以等定时器的回掉执行时，打印的是之前闭包中存储的变量。  

**如何避免拿到旧的prop或者state？**
- 使用useRef
- 查看是否遗漏了依赖, 导致effect没有更新
