## Obsidian 格式化方案

```ad-tip
title: [Linter](https://github.com/platers/obsidian-linter) 插件

原因：可定制化非常强，基本满足我的格式化要求

缺点：全英文的配置界面确实有点难顶啊 😵‍💫
```

### 配置简单说明

- [x] [add-blockquote-indentation-on-paste](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#add-blockquote-indentation-on-paste)：给复制到引用内容的多行文本，每行前面添加一个引用符号 `>`
- [x] [space-between-chinese-japanese-or-korean-and-english-or-numbers](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#space-between-chinese-japanese-or-korean-and-english-or-numbers)：中文日文或韩文与英文或数字之间的空格
- [x] [consecutive-blank-lines](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#consecutive-blank-lines)：空行转换，最多只能存在一个连续的空行
- [x] [empty-line-around-blockquotes](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#empty-line-around-blockquotes)：确保 blockquote（块引号）周围存在一个空行，除非它们在文档的开始或结束位置
- [x] [empty-line-around-tables](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#empty-line-around-tables)：确保表格周围存在一个空行
- [x] [heading-blank-lines](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#heading-blank-lines)：确保标题前后的空行
- [x] [line-break-at-document-end](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#line-break-at-document-end)：确保文档末尾有且只有一个空行
- [x] [paragraph-blank-lines](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#paragraph-blank-lines)：确保段落之间存在一个空行
- [x] [space-after-list-markers](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#space-after-list-markers)：普通列表（有序、无序）和任务列表标记后应该有一个空格
- [x] [remove-consecutive-list-markers](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-consecutive-list-markers)：删除连续的列表标记，比如 `- -` 变成 `-`
- [x] [remove-empty-list-markers](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-empty-list-markers)：删除没有使用的列表标记
- [x] [remove-empty-lines-between-list-markers-and-checklists](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-empty-lines-between-list-markers-and-checklists)：删除普通列表与任务列表之间的空行
- [x] [remove-link-spacing](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-link-spacing)：删除链接文本周围的间距（Markdown image 语法 `![xxx  ]()` 不受影响）
- [x] [trailing-spaces](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#trailing-spaces)：删除每行尾部多余的空格
- [x] [remove-multiple-spaces](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-multiple-spaces)：将一行中多个空白行合并为一个
- [x] [proper-ellipsis](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#proper-ellipsis)：使用省略号替换三个 `.`
- [ ] [no-bare-urls](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#no-bare-urls)：用尖括号将裸 URL 括起来，除非用反引号、方括号或单引号或双引号括起来（会变得很奇怪）
- [ ] [remove-space-around-characters](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-space-around-characters)：删除全角字符周围的空格和制表符（会导致全角符号后面跟了标签会被删除空格，使得标签无法正确被识别，暂时不用了）

