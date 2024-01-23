## 前言

2023-12-08 目前基本都不用啦~ 全部换成普通的引用形式。

Callout 是 Obsidian 自带的引用卡片样式，Admonition 是第三方插件，指定格式，由不同的关键字触发。

相信通过上面的两个 Admonition 块与文档前面的 Callout 对比，在 Admonition 图标上已经能够看到与 Callout 图标的区别了，外观差不多，只不过一个实心图标，一个空心图标，我比较喜欢实心的，而且 Admonition 明显做的更好，图标与标题垂直居中对齐，Callout 的图标位置明显偏下了，虽然我可以通过 CSS 调整，但也不是人人都会，随便就能改的，就这样吧，后续考虑换掉！我甚至还发现默认提供的 Callout 在来回切换文档时候会刷新，闪动一下，貌似重新渲染了？

> 样式预览

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Obsidian-Callout%20%E6%A0%B7%E5%BC%8F%E5%AF%B9%E6%AF%94.png)

## Callout

书写格式：

在 `> [!Type]` 的后面添加一个 "+" 中间不要添加空格，可以把 Callout 变成一个可折叠块且默认展开，反之一个 "-"，那么就是默认折叠。

```text
> [!Type] 简略的标题内容
>
> 更多的内容（可以不写，我一般不写）
```

**Type** 关键字对应样式展示：

> [!note] note

> [!tldr] abstract | summary | tldr

> [!info] info | todo

> [!tip] tip | hint | important

> [!success] success | check | done

> [!faq] question | help | faq

> [!warning] warning | caution | attention

> [!failure] failure | fail | missing

> [!danger] danger | error

> [!bug] bug

> [!example] example

> [!quote] quote | cite

> 下面这个 todo 貌似是新增的？我乱写了下居然有！

> [!todo]

## Admonition

这里顺便介绍一下 Admonition，一个和 Callout 快大差不差的美化卡片显示的插件（是官网 Callout 出现前的方案）

1. 写法、操作习惯，以及默认提供的类型图标样式上稍微有一点点区别
2. Admonition 拥有定制能力，可以自定义图标与样式（这点对于喜欢自己动手的小伙伴来说还是蛮香的）

首先看写法上：从大于号的引用块变成了代码块，然后在代码块内部写上 `ad-` 加 Type 关键字（请参考 Callout Type），内部也配置了一些参数，如下：

````text
```ad-[TYPE]
title: 标题
collapse: 折叠状态（open/clsoe/none)

内容巴拉巴拉...
```
````

其次是使用习惯上，Callout 使用鼠标点击一下内部即可进入编辑（会自动全选整个 Callout 块），Admonition 是必须点击右上角的 `</>` 显示源码按扭才能进入编辑

```ad-tip
title: tip
collapse: open

content
```

```ad-note
title: 内部的代码高亮

- js
~~~JavaScript
console.log('Hello World')
~~~

- python
~~~python
print("Hello World")
~~~
```
