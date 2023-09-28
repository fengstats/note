## 元素和属性

### 基础元素

- `<header>`：头部
- `<nav>`：导航
- `<section>`：定义文档某个区域的元素
- `<article>`：内容元素（文本内容偏多）
- `<aside>`：侧边栏
- `<footer>`：底部

### 媒体类型元素

- `<audio>`：音频
  - autoplay：是否自动播放，主流浏览器基本禁止，原因也很简单，你也不希望你打开某不知名小网站时被突如其来的声音社死吧
  - muted：是否禁音，当然，如果把这个属性设置为 `true` 那么就可以自动播放了
  - preload：是否需要预先加载视频，`none/auto/metadata`
- `<video>`：视频（属性参数与 audio 基本一致，也多了一些杂七杂八的你用不到的属性）

### input 元素的扩展

- placeholder：输入框内的占位文字
- multiple：多个值
- autofocus：自动聚焦

type：`date/time/number/tel/color/email` 等等，[MDN 文档](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input)

### 全局属性 data-\*

> 用于自定义数据

- 通过 `data-*` 的属性可以在 JS 的 DOM 操作中通过 `dataset` 获取
- 通常用于 HTML 和 JS 之间的数据传递

```html
<div class="box" data-name="chen" data-age="18">box</div>

<script>
  const boxElement = document.querySelector('.box')
  console.log(boxElement.dataset)
</script>
```

## CSS 函数

如我们之前使用过的 `rgb/rgba/translate/rotate/scale` 等等 CSS 函数

继续学习几个好用的 CSS 函数

var：使用 CSS 定义的变量

属性名需要使用两个减号开头，如 `--main-color: red;`，使用 `color: var(--main-color)`（注意：只有后代元素才能使用）

calc：计算 CSS 值，通常用于计算元素的大小或位置

blur：毛玻璃（高斯模糊）效果

gradient：颜色渐变函数

## BFC

## 媒体查询
