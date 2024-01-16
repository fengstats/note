**提示**：切换分支即可查看对应版本实现代码。

## 01-13 打卡

### 学习

1. 关于虚拟 DOM 数据结构设计以及抽象思想。
2. 在 JSX 中使用 `<App />` 形式组件时其实默认会去寻找 `React.createElement` 方法调用；
3. 生成虚拟 DOM 对象数据返回，也就是说这里的 JSX 本质上就是 `React.createElement` 的语法糖。
4. 是 Vite 中 ESBuild 的 Babel 插件帮助我们完成了这件事情。

### 问题

写到动态生成的 vDom 时，对数据结构设计不清晰导致频频卡壳。

### 解决

观察 v0.1 中写死代码的相同之处与不同之处，抽离属性，罗列并尝试代入 vDom 看是否可通用。

### 课后问题延伸

**如何自定义 JSX 解析方法名称呢？**

1. 通过 JSX pragma 在文件顶部进行标注，注意如果其他地方要使用更改后的名称同样需要定义

```js
// App.jsx
/**@jsx FReact.createElement */
import FReact, { createElement } from './core/React'

// ƒ AppFunc() {
//   return /* @__PURE__ */ FReact.createElement("div", { id: "newApp" }, "mini react");
// }
function AppFunc() {
  return <div id='newApp'>mini react</div>
}
```

2. 通过 Vite 配置文件更改默认 Babel 解析方法名称，这是全局配置生效

```js
// vite.config.js
import { defineConfig } from 'vite'

export default defineConfig({
  esbuild: {
    jsxFactory: 'CReact.createElement',
  },
})
```

**我们自己实现的 render 方法递归可能会导致浏览器卡顿？**

应该是 DOM 树嵌套层级太深，导致计算量很大导致的，用 Fiber 架构实现任务调度来分批执行可以解决，也就是第二天的学习内容哈哈哈。

### 代码

- [v0.1](https://github.com/fengstats/mini-react/tree/v0.1)
- [v0.2](https://github.com/fengstats/mini-react/tree/v0.2)
- [v0.3](https://github.com/fengstats/mini-react/tree/v0.3)
- [v0.3-jsx](https://github.com/fengstats/mini-react/tree/v0.3-jsx)

## 01-14 打卡

### 学习

1. 浏览器基础知识，认识到 JS 是单线程执行的，逻辑代码量过大时会造成阻塞。
2. 一个新的浏览器 API `requestIdleCallback`，可以传入函数，会在浏览器空闲时间执行。
3. 拆分任务的思想，大任务拆成小任务，小任务转换为立即行动。
4. 把 DOM 树转换成平铺的链表结构，怎么去设计数据结构和怎么去更改指向。

### 问题

Fiber 架构的概念有点难懂。

### 解决

对于树转换链表那一块的知识其实还好，因为刷了不少链表 + 指针相关的算法题目，所以理解起来没那么费力，不过 Fiber 架构不一样，应该算是第一次正式了解它，主要还是从几个方面

1. Fiber 架构是什么？一个任务调度器，拆分任务在空闲时间内执行。
2. 它的历史？// TODO
3. 它的出现解决了那些问题？优化 DOM 嵌套层级很深时的渲染问题。
4. 怎么去实现一个最简 Fiber？利用 `requestIdleCallback` API。

### 课后问题延伸

因为目前实现的 Fiber 架构是边转换 DOM 边进行渲染的，所以在实际渲染过程中可能会出现用户看到渲染了一半的 DOM 元素，此时浏览器没有空余时间了，卡住过一会才完成全部渲染。

这个问题可以在所有的 children 转换完成之后进行统一提交添加 DOM 来解决。

### 代码

- [v0.4](https://github.com/fengstats/mini-react/tree/v0.4)

## 01-15 打卡

### 学习

1. 遇到问题先找 **why**，知道问题的原因就好解决了。
2. 看源码就是为了学习别人解决路，而不是去背代码。
3. 学习完后消化，并且在业务问题的场景中使用出来才是你自己的能力。

### 问题

### 解决

### 课后问题延伸

### 代码
