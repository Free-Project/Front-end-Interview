# React中useEffect(fn, [])和ComponentDidMount的区别
hook和生命周期方法基于完全不同的原理。 诸如componentDidMount()类的方法围绕生命周期和渲染时间展开，而useEffect(fn, [])则围绕状态和与DOM的同步进行设计。
