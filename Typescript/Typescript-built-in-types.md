# Typescript实用的内置类型

typescript 提供了很多实用内置的类型，大家安装typescript 的时候，可以在node-module/typescript/lib/文件下面有对js 所有的声明文件，包含es5,es6...到最新的esnext 版本，本篇主要是总结一下对typescript 实用内置类型的笔记，比如 官方文档给出的这些：

- `Exclude<T, U>` -- 从T中剔除可以赋值给U的类型。
- Extract<T, U> -- 提取T中可以赋值给U的类型。
- NonNullable<T> -- 从T中剔除null和undefined。
- ReturnType<T> -- 获取函数返回值类型。
- InstanceType<T> -- 获取构造函数类型的实例类型。
