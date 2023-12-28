# TypeScript 入门

## 前言

- [林不渡 - TypeScript 入门教程](https://juejin.cn/book/7288482920602271802) - 用简单自然的方式入门 TypeScript
- [TypeScript Playground](https://www.typescriptlang.org/zh/play) - 一个用于 TypeScript 和 JavaScript 的在线编辑器。

## 扩展

- [TypeScript Importer](https://marketplace.visualstudio.com/items?itemName=pmneo.tsimporter) - 收集项目内的所有定义，敲出 `:` 时提供类型补全并自动导入。
- [Pretty TypeScript Errors](https://marketplace.visualstudio.com/items?itemName=yoavbls.pretty-ts-errors) - 更好看的 TypeScript 错误提示。
- [Move TS](https://marketplace.visualstudio.com/items?itemName=stringham.move-ts) - 移动文件路径后，自动更改项目内文件链接路径。

## 运行

- [tsx](https://github.com/privatenumber/tsx) - 增强 Node.js 以运行 TypeScript 文件，支持 ESM 模块化。

```shell
npx tsx index.ts
```

- [esno](https://github.com/esbuild-kit/esno) - 原理也是先编译再执行的过程，只不过底层使用的是 ESBuild 所以速度很快，而且托尼的项目！

> ⚠️ v0.15 开始，就是 tsx 的别名了，功能都一样，所以还是推荐 tsx。

```shell
npx esno index.ts
```
