## Obsidian 格式化方案 Linter

> [!tip] [Linter](https://github.com/platers/obsidian-linter) 插件
>
> 原因 - 可定制化非常强，基本满足我的格式化要求
>
> 缺点 - 全英文的配置界面确实有点难顶啊 😵‍💫

> 2023-11-30 补充：已经有中文配置界面啦 🥳！

### 启用

- [proper-ellipsis](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#proper-ellipsis) - 使用省略号替换三个 `.`。
- [heading-blank-lines](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#heading-blank-lines) - 确保标题前后的空行。
- [trailing-spaces](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#trailing-spaces) - 删除每行尾部多余的空格。
- [paragraph-blank-lines](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#paragraph-blank-lines) - 确保段落之间存在一个空行。
- [empty-line-around-tables](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#empty-line-around-tables) - 确保表格周围存在一个空行。
- [remove-empty-list-markers](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-empty-list-markers) - 删除没有使用的列表标记。
- [remove-multiple-spaces](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-multiple-spaces) - 将一行中多个空白行合并为一个。
- [line-break-at-document-end](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#line-break-at-document-end) - 确保文档末尾有且只有一个空行。
- [consecutive-blank-lines](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#consecutive-blank-lines) - 空行转换，最多只能存在一个连续的空行。
- [remove-consecutive-list-markers](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-consecutive-list-markers) - 删除连续的列表标记，比如 `- -` 变成 `-`。
- [space-after-list-markers](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#space-after-list-markers) - 普通列表（有序、无序）和任务列表标记后应该有一个空格。
- [add-blockquote-indentation-on-paste](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#add-blockquote-indentation-on-paste) - 给复制到引用内容的多行文本，每行前面添加一个引用符号 `>`。
- [empty-line-around-blockquotes](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#empty-line-around-blockquotes) - 确保 blockquote（块引号）周围存在一个空行，除非它们在文档的开始或结束位置
- [remove-link-spacing](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-link-spacing) - 删除链接文本周围的间距（Markdown image 语法 `![xxx  ]()` 不受影响）
- [remove-empty-lines-between-list-markers-and-checklists](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-empty-lines-between-list-markers-and-checklists) - 删除普通列表与任务列表之间的空行。
- [space-between-chinese-japanese-or-korean-and-english-or-numbers](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#space-between-chinese-japanese-or-korean-and-english-or-numbers) - 中文日文或韩文与英文或数字之间的空格。

## 禁用

- [no-bare-urls](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#no-bare-urls) - 用尖括号将裸 URL 括起来，除非用反引号、方括号或单引号或双引号括起来（感觉有点奇怪）。
- [remove-space-around-characters](https://github.com/platers/obsidian-linter/blob/master/docs/rules.md#remove-space-around-characters) - 删除全角字符周围的空格和制表符，会导致全角符号后面跟了标签会被删除空格，使得标签无法正确被识别，暂时不用了。

> 目前我对 Dataview 的了解以及想法 💭

看了看，这个插件就是类似写 SQL 语句一样去过滤你的 Obsidian 数据，拿到你想要的数据后，只要你会写，配合 JS + CSS 就能把数据展示的五花八门，同时还提供了 dataviewjs，也就是可以用 JS 代码来操作（毕竟我会点 JS，这个参考一些基本就能用起来了），但在我准备开始折腾的时候又想了想 🤔，对我而言是否真的有需要？是否值得我花大量的时间去学习与使用？

答案是否定的，原本打算让 dataview 处理我日常记录中任务事项的时间计算，以及显示一些当天未完成的任务之类的，但是 dataview 只能在 Obsidian 中显示，那我用网页 GitHub 或者迁移到其他软件时，岂不是只能看到一串代码，想到这，突然就不想写了。

所以，最后还是打算自己写个 node 脚本将实际的数据处理一下，这样无论后面怎么迁移笔，这个数据都是真实存在的，不过得好好想想这个脚本改如何写好一点，如何能让我更加便捷的使用，头疼~ 🤯

15:20 体验了下这个插件 [Code Styler](https://github.com/mayurankv/Obsidian-Code-Styler)，是和 CodeBlock 样式有关的，找这个插件是因为我发现如果在有 CodeBlock 代码的笔记来回切换时，会导致文件笔记内容位置突然变化（增高），然后迅速恢复，一开始我以为是我写的 CSS 样式可能加了动画影响到了，关了还是这样，尝试这个插件也没用，后面更新了下 Obsidian 版本，貌似体验好了点。

Obsidian 的代码块 DOM 没有父元素，是每块（行）有一个 DOM 渲染的，还好看到有个 begin 和 end 的类标识（首尾块），直接一个 `border-top` 加 `border-bottom`，剩下 `left+right` 完事。

> Obsidian pdf 导出图片模糊化

13:00 是一个 `Privacy Glasses` 的插件导致的，还有一个问题是粘贴到本地图片路径自动简短化了，配置问题，可以在设置中配置为“相对路径地址”

11:30 [大纲美化 V3 修复版 - 经验分享 - Obsidian 中文论坛](https://forum-zh.obsidian.md/t/topic/19837)

15:35 Obsidian 里面的 **vimrc** 支持可算是折磨死我了，我就单纯想把 `gg` 映射成 `ggzz`，换成系统中的 vimrc 那一下就好了，在这里就是死活不生效，也没什么报错之类的提示，搞得我无从下手只能一点点看是不是自己写错了，从 map、nmap、nnoremap、exmap 慢慢试，不行，去官网看看有没有类似例子说明，也没有，看 Issues，太多了看不明白，最后报着试一试的心态写了个 `nmap gg 1Gzz`，行……了？真无语啊！😤 我想知道这有啥区别啊，凭啥我前面的不行啊，不响完辣！这破玩意东西真不能折腾，一弄起来真的没完。

### Obsidian

> [!todo] Calendar 日历显示问题

本来是准备补充一下昨天的笔记的，我一看 Calendar 插件每日任务状态图标这个显示不对啊，按照我平常的使用习惯来说，一个实心点 + 一个空心点就是有任务选项没有完成，一个实心点就是都完成了，怎么有这么多实心点。然后我新建了一个未命名笔记做测试，把数据剪贴出去，恢复正常，粘贴进来，还是这样，重启 Obsidian 无果，我就一个段落一个段落的复制粘贴，我倒要看看究竟是什么出的问题，最后找到了是 table 表格在作怪，很奇怪，我没有找到固定的影响实心点多出的套路，但是能肯定就是这个影响的。准备了几个 table 表格，先在第一个 table 添加数据，到 12 行就多了一个，然后再怎么添加都没效果了，第二个 table 表格到 4 行就多一个了。到这里我知道不该浪费时间继续下去了，毕竟我不是软件开发者，这也仅仅是个显示问题，对我的使用影响不大，还没到去提 issues/pr 的地步，希望后面更新能修复吧，或者有空了我自己来深入看一下 Calendar 插件的代码，尝试修复这个问题，目前没时间，就单单记录一下。

![](attachments/05-06%20周六_calendar_显示异常.png)

> Obsidian Memos 调整前后对比

![](attachments/05-05%20周五_memos_调整前后对比.png)

> Obsidian 日记多层目录

![](attachments/05-05%20周五_日记多层目录.png)

### Obsidian Plugin

> CheckList 设置中排除目录、包含目录的规则写法示例

```text
{,!(01-Templates)/**}
{,2023/**,2024/**}
```

> [!info] Omnisearch 体验说明
>
> 说实话，简单体验了下觉得自带的搜索做的挺不错的了，暂时没有痛点需要增加额外的搜索插件解决，就先关掉了，另外和它配套的一个分词貌似还不错，支持 Vim Mode 的分词光标移动我比较感兴趣，启用体验一阵子再说

> [!bug] TODO: Obsidian 全局搜索重复点击同个搜索结果时整个软件会出现闪屏现象

今天遇到的一些问题

> [!todo] 标题块卡住 Vim 移动（gj/gk）

经过开发工具调试，排查应该是 margin-block 属性所影响，具体原因未知，先取消掉该设置临时解决问题，后续有时间的话再来看看。

> [!todo] Style Settings 变量形式需要手动设置一次

当前行与代码块背景我配置成可选择的颜色设置选项了，但是让我非常疑惑的就是我必须要手动去设置一次才能把变量加载到 Obsidian 中（还找了好久），因为这个并不是我目前的重点，所以就先这样，能用就行，配置方式是参考官方的 [Style Settings](https://github.com/mgmeyers/obsidian-style-settings#obsidian-style-settings-plugin)

02:50 学到了，插件与插件之间可以做到的骚操作，具体视频请看：[Obsidian 城堡系列第 2 弹 - bilibili](https://www.bilibili.com/video/BV12k4y1n7tU?t=105.1)

1. 先通过 Commander 插件设置 Macros 宏命令
2. 先设置打开 Style Settings 页面（Show style settings view）
3. 设置 Delay（50 就够了）
4. 设置 Hover Editor 插件的命令，将当前活动页面转换为悬浮页面（Convert active pane to Hover Editor）

这样就可以无痛调试样式了，不需要来回切页面，真不错啊。

### Obsidian Git

其实很简单，就是配置当前电脑免密 ssh 连接。

> GitHub 在我测试 Obsidian Git 插件 push 的时候突然挂了，搞得我还以为是我自己的仓库出问题了

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20231204204346.png)

> 生成 ssh 密钥（-C 后面的邮箱换成自己的）：生成后找到你的公钥文件，把里边的内容添加到你自己的 👉🏻 [GitHubSSH keys](https://github.com/settings/keys) 即可

```shell
ssh-keygen -t rsa -C "feng2860984180@163.com"
```

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Shell%20%E7%94%9F%E6%88%90%20ssh%20%E5%AF%86%E9%92%A5.png)

> 更改邮箱地址

我是直接在 Settings -> Emails -> Add email address 添加上了这个邮箱，下图中的解决方案应该也是可行的：

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20231204204457.png)

> 快捷键

> [!tip]
>
> 1. 设置打开 Finder 快捷键：`cmd+alt+r`
> 2. 设置上下行互换快捷键：`alt+jk`
> 3. 模板标题语法设置
> 4. File Explorer Note Count：显示笔记数量
> 5. Recent Files：近期打开笔记，展示一个列表用于快速切换
> 6. Obsidian Memos：和语雀的小记一样，一个快速记忆零散知识的东西
> 7. 搜索关键词：
> 8. 直接搜索：1
> 9. 包含多个关键词的文档（空格隔开）：1 2
> 10. 包含某一个关键词的文档（OR）：1 OR 2
> 11. 指定搜索范围：文件名（file:1）、文本内容（content:1）、标签（#tag:1）
> 12. 搜索同一行的多个关键词：line: 1 2
> 13. 搜索任务：
> 14. 直接搜索：task:1
> 15. 搜索未完成任务：task-todo:1
> 16. 搜索已完成任务：task-done:1
> 17. 保存搜索结果展示到笔记中，先创建一个语言为 query 的代码片段，并使用上述搜索语言编写搜索代码，回车后，如下所示：

```query
task: v
```

> Obsidian 中 VScode 快捷键方案配置

1. 前进后退：Cmd + \[ / \]
2. 上下左右分屏：Cmd + \\, Cmd + Shift + \\
3. 上下左右聚焦：Cmd + Shift + hjkl
4. 创建/切换近期文件：Cmd + P
5. 调出系统控制面板：Cmd + Shift + P
6. 当前文件重命名：Cmd + Shift + R

2023-05-24 发布了 Obsidian 新版本 v1.3.3，还没注意就直接自动更新了，看一眼笔记，诶，我的「大纲美化」和「Recent Files」样式怎么不对劲了，猜测应该是某些类属性或者元素结构变更了，简单过了下更新说明，这个版本也没什么吸引我更新的功能（还有之前闪屏的 bug 也没修复），所以直接回退到了 [v1.2.8](https://github.com/obsidianmd/obsidian-releases/releases/tag/v1.2.8)

> 操作步骤：

1. 先卸载当前的 Obsidian（我用的 Tencent Lemon，会帮助清理一些缓存文件之类）
2. 在 GitHub 下载指定版本的安装包
3. 断网！断网！断网！（如果不断网，下次重新启动还会自动更新安装最新新版本）
4. 安装 Obsidian，打开自己的 vault 仓库
5. 打开设置，找到 About（关于）=> App（应用）=> Automatic updates（自动更新）关闭

做完这些之后就可以联网同步使用了

> 自定义快捷键

- 有序列表：Command + O
- 无序列表：Command + J
