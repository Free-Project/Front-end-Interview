
## void 和 undefined 有什么区别？
TypeScript中void类型是any类型的子类型，是null和undefined类型的父类型。  

void类型的变量值是有限制的，只能是undefined和null。如：
```
let a: void = null;
let b: void = undefined;
```

## 什么是 never 类型？
never 表示一个不包含值的类型，即表示永远不存在的值。

## never 和 void 的区别
void 表示没有任何类型（可以被赋值为 null 和 undefined）。
void 类型的函数，主要是用在不关心函数返回值的情况下，比如通常的异步回调函数，这种情况下返回值是没有意义的。

never 表示一个不包含值的类型，即表示永远不存在的值。

拥有 void 返回值类型的函数能正常运行。
拥有 never 返回值类型的函数无法正常返回，无法终止，或会抛出异常。

## 下面代码会不会报错？怎么解决？
const obj = {
    a: 1,
    b: 'string',
};
  
obj.c = null;

## readonly 和 const 有什么区别？
1. const 关键字只能在常量声明中初始化。 readonly 字段可以在声明或构造函数中初始化，因此，根据所使用的构造函数，readonly 字段可能具有不同的值。
2. const 字段是编译时常量，而 readonly 字段可用于运行时常数。
3. const 默认就是静态的，而 readonly 如果设置成静态的就必须显示声明。
4. const 对于引用类型的常量，可能的值只能是 string 和 null，readonly 可以是任何类型

## 下面代码中，foo 的类型应该如何声明
```
function foo (a: number) {
    return a + 1;
}
 
foo.bar = 123;
```

## 下面代码中，foo 的类型如何声明
```
let foo = {};
  
for (let i = 0; i< 100; i++) {
    foo[String(i)] = i;
}
```

## 实现 MyInterface
```
interface MyInterface {
    ...
}
class Bar implements MyInterface {
    constructor(public name: string) {}
}
class Foo implements MyInterface {
    constructor(public name: string) {}
}
  
function myfn(Klass: MyInterface, name: string) {
    return new Klass(name);
}
  
myfn(Bar);
myfn(Foo);
```

## 什么是 Abstract Class？

## 什么是 class mixin, 如何实现？

## typeof 关键词有什么用？
ypeof操作符可以用来获取一个变量或对象的类型。

## keyof 关键词有什么用？

## 下面代码中，foo 的类型如何声明
function fn(value: number): string {
    return String(value);
}
const foo = fn;

## 下面代码会导致 TS 编译失败，如何修改 getValue 的类型声明。
```
function getValue() {
    return this.value;
}
  
getValue();
```

## 下面是 vue-class-component 的部分代码，解释为什么会有多个 Component 函数的声明，作用是什么？TS 官方文档的那一节有对应的解释文档？
```
function Component <U extends Vue>(options: ComponentOptions<U>): <V extends VueClass>(target: V) => V
function Component <V extends VueClass>(target: V): V
function Component <V extends VueClass, U extends Vue>(
 options: ComponentOptions<U> | V
): any {
  if (typeof options === 'function') {
    return componentFactory(options)
  }
  return function (Component: V) {
    return componentFactory(Component, options)
  }
}
```

## 如何声明 foo 的类型？
```
const foo = new Map();
foo.set('bar', 1);
```

## 如何声明 getProperty，以便能检查出第八行将会出现的运行错误。
```
function getProperty(obj, key) {
    return obj[key].toString();
}
 
let x = { a: 1, b: 2, c: 3, d: 4 };
 
getProperty(x, "a");
getProperty(x, "m");
```

## 类型声明里 「&」和「|」有什么作用？

## 下面代码里「date is Date」有什么作用？
```
function isDate(date: any): date is Date {
  if (!date) return false;
  return Object.prototype.toString.call(date) === '[object Date]';
}
```

## tsconfig.json 里 --strictNullChecks 参数的作用是什么？

## interface 和 type 声明有什么区别？
参考 https://github.com/kothing/Front-end-Interview/blob/main/TypeScript%E4%B8%ADinterface%E5%92%8Ctype%E7%9A%84%E5%8C%BA%E5%88%AB.md

## 如何完善 Calculator 的声明。
```
interface Calculator {
    ...
}
 
let calcu: Calculator;
calcu(2)
  .multiply(5)
  .add(1)
```

## 「import ... from」、「 import ... = require()」 和 「import(path: string)」有什么区别？

## declare 关键字有什么用？

## module 关键字有什么用？

## 如何处理才能在 TS 中引用 CSS 或者 图片使之不报错？
```
import "./index.scss";
import imgPath from "./home.png";
```

## 编写 d.ts 来声明下面的 js 文件
```
class Foo {
}
module.exports = Foo;
module.exports.Bar = 1;
```

## namespace 和 module 有什么区别

## 如何实现 module alias?编译成 JS 能否直接运行？
```
import Bar from '@src/Bar';
```

## 哪些声明类型既可以当做 type 也可以当做 value？
