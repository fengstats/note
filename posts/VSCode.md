2024-03-21 TypeScript Import 报错

```bash
 Notification handler 'namespaceUpdate' failed with message: this._namespaceCache[file.namespace].push is not a function
```

关于 VSCode package.json 中 script 脚本上面提供的一键启动按钮消失了的问题

```json
// jsonc 不会被识别
"files.associations": {
  "*.json": "jsonc"
}
```

2024-01-25

- [To TS Type](https://marketplace.visualstudio.com/items?itemName=simonhe.to-ts-type) - 通过 Command+Option+T 快捷键将复制的数据转换成对应的 TS 类型。
- [Fast Jump](https://marketplace.visualstudio.com/items?itemName=simonhe.fast-jump) - 通过 Command+E 在变量或者函数上一步跳转到位。
- [TailwindCSS Highlight](https://marketplace.visualstudio.com/items?itemName=ellreka.tailwindcss-highlight) - 提供 TaliwindCSS 样式的高亮背景，可以针对自己比较关注的样式配置突出显示。

2024-01-18 VSCode 插件

- [Apc Customize UI++](https://marketplace.visualstudio.com/items?itemName=drcika.apc-extension) - 自定义你的 VSCode 界面，提供 JS CSS 注入功能，可用于 Animations 插件。
- [VSCode Animations](https://marketplace.visualstudio.com/items?itemName=BrandonKirbyson.vscode-animations) - 可定制的动画扩展，我主要用它的光标。
- [matchit](https://marketplace.visualstudio.com/items?itemName=redguardtoo.matchit) - 代替原生 Vim 的 % 功能，匹配范围更精确且支持匹配 html 标签，映射键配置为 S。

---

- [Hungry Delete](https://marketplace.visualstudio.com/items?itemName=jasonlhy.hungry-delete) - 更加智能的 Backsapce，增加了 Option+Backspace 删除前面所有空行快捷方式
- [TS 自动引入](https://marketplace.visualstudio.com/items?itemName=kevinmcgowan.TypeScriptImport)
- [TS 移动文件后自动更新引入位置](https://marketplace.visualstudio.com/items?itemName=stringham.move-ts)

> 关于 VS Code 中使用 iTerm 作为终端部分命令输出后色彩丢失

[zimfw/utility](https://github.com/zimfw/utility/issues/2) 找到了！就是这个插件刺客，内置扩展启动的时候往 VS Code 里面注入了 NO_COLOR=1，直接让我部分命令输出颜色丢失了，可以通过关闭这个插件或者在 settings.json 中设置

```shell
"terminal.integrated.env.osx": {
  "NO_COLOR": null
},
```

> 解决群友问题

其实就是不同系统注入 wepback 环境变量的方式有所不同罢了，这个项目内置命令本身是提供给 unix 系统的，小伙伴用的是 win

- 在 windows WSL 中使用
- 调整一下命令：添加 `set` 前缀或者安装 `cross-env` 依赖包配置下（一个跨平台的环境变量配置工具）

我翻了下这个仓库的 issues 貌似也有这个问题的解答：[#687](https://github.com/heartexlabs/label-studio-frontend/issues/687)

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20231204213426.png)

> flash.vim 问题

在 `*.md` 文件中使用 `flash.vim` 写了点匹配词后，通过 backspace 删除更改，发现无反应，只能用 Esc 退出 flash，测试其他类型文件没有发现这个问题。

13:45 VSCode 小技巧：`^\s*\n` 可以替换空行

- 17:40 我把系统提供的选项卡切换前后 tab 的快捷键重新定义了，设置了只能在组内切换，在终端使用时发现终端的这个快捷键也被影响了，于是就只能重新在终端出定义一遍，写上 when 条件，后续在看看有没有好的解决方案吧。

![](attachments/06-07%20周三_vscode_terminal_keybinding.png)

- 20:48 **background-cover** 这个插件还是蛮不错的，显著提升编程幸福度 🌟。

![](attachments/theme-SpacegrayEightiesDark.png)

- 15:00 改看分屏快捷键的时候发现了这个，可惜对全键盘用户并不友好，需要鼠标参与才能来回聚焦，浏览源码的时候当前文件过长时需要上下来回切可以用这个，不会创建新的编辑组，会在当前组聚焦的编辑文件内分离一个副本浏览。

![](attachments/06-07%20周三_vsocde1.png)

- 12:45 关于 Animations: Scrolling 失效的问题，简单去看了下这个库，最近更新时间是今天凌晨五点左右，应该是这次更新出的问题，算了，我解决不了，看仓库 commits 仓库还蛮新的，也就半个月之前提交的第一个 commit，更新频率还行，那就等仓库作者下次更新吧，本来想提个 issue， 但是作者不是中国人，我怕我机翻的英文词不达意，呜呜呜。

```json
// snippets 导致补全异常的问题
"editor.suggest.snippetsPreventQuickSuggestions": false
```

配置 git 快速打开当前文件更改对比快捷方式：leader + df

snippets 的学习

1. [VS Code snippets 官方文档](https://code.visualstudio.com/docs/editor/userdefinedsnippets#_snippet-scope)
2. [snippets 生成工具](https://snippet-generator.app/)
3. 注意几个点（Tab 后的位置、变量的使用、默认值、多个光标）

重构方面（内置自带命令：⌘ + .）

1. 选中一个代码片段抽离成函数
2. 选中一段内抽离成变量
3. hocus pocus（自定义 leader + ff 创建函数，leader + vv 创建变量）

> 显示函数的参数提示：⌘ + shift + space

19:05 VS Code | 呼出系统命令面板输入 "toggle screencast mode" 内置的按键提示功能还蛮好看的

VS Code 多光标快捷键：Command + Option + 上下箭头

> VS Code 插件：Format Files

稍微配置下需要忽略的文件夹，自定义格式化文件类型（当然也可以不配置，就是会把所有文件格式化，可能会比较慢），配置完成后，点击右键需要格式化的文件夹就能看到 **Strat Format Files: This Folder**，插件初步扫描需要格式化文件后会弹窗，选择 **Do it!** 开始格式化，虽然这个插件貌似比较久了，但是满足我的需求就足够了

Vue 项目中子组件和组件库标签的颜色关键字

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/VSCode%20Vue%20%E5%AD%90%E7%BB%84%E4%BB%B6%E9%A2%9C%E8%89%B2%E5%85%B3%E9%94%AE%E5%AD%97.png)

BackSpace（退格键）在 Vim 的选中模式配置

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/VSCode%20Vim%20BackSpace%20%E9%80%89%E4%B8%AD%E6%A8%A1%E5%BC%8F%E6%98%A0%E5%B0%84.png)

群友问我配置文件中的注释怎么写的？我：手敲的

不过倒也确实提醒我了，这种事情为什么不能写个 snippets 来帮我做呢，说干就干，挺简单的就几行代码

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/VSCode%20Snippets%20Comment.png)

关于 `.vue` 文件部分代码高亮丢失问题

没办法演示了…看情况应该是 **Vue Language Features (Volar)** 修复了，昨天反复测试发现明明是被 **Babel JavaScript** 这个插件所影响的，为此我甚至关掉了我所有的配置恢复默认，今天打算复现一下，好了，直接无效，好像就是刚刚一会更新的，无语辣！

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20231204200534.png)

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20231204200551.png)

## Comment Anchors

一个注释锚点高亮的插件，应用侧边栏多出的 icon 可以让你快速定位到当前工作区你所打上锚点的文件位置，你可以自定义你的 tags（锚点标签），配置是否启用、作用域以及其他样式即可，以下是我配置的一些效果：

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/VSCode%20Anchors%20%E6%95%88%E6%9E%9C%E5%9B%BE.png)

## Codeium

一个类似 GitHub Copilot 的代码智能提示插件，优点是免费，我上次弄了蛮久没效果，今天突发奇想弄一下，结果就能用了…有点迷

后续补充：找到问题所在了，我把内联建议直接关掉了（如下图所示），这还怎么让别人提示，我的问题我的问题，当时是我太大声了，对不起 🙏

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/VSCode%20%E5%86%85%E8%81%94%E5%BB%BA%E8%AE%AE%E9%80%89%E9%A1%B9.png)

> 下面是其他的

```json
"editor.quickSuggestions": {
  // 是否在你打注释的时候给你提示建议
  "comments": "off",
  // NOTE: 是否在你输入字符的时候给你提示建议，解决了我模板字符串内变量不提示的问题
  "strings": "on"
},
```

17:55 直接在配置文件中设置 `"diffEditor.renderSideBySide": false`，也可以通过打开对比编辑器右上角的三个小点来更改，默认是两个编辑器来对比（左右），内联视图就是把内容全部在一个编辑器中显示，我有时候自己会打开多个编辑组，这样看对比编辑器时就会感觉很小，所以就改成内联视图了。

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/VSCode%20%E5%86%85%E8%81%94%E8%A7%86%E5%9B%BE.png)

补一张默认的吧：

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/VSCode%20%E5%A4%9A%E7%AA%97%E5%8F%A3%20Diff%20%E9%BB%98%E8%AE%A4%E8%A7%86%E5%9B%BE.png)

> until explicitly set to be kept open (via double-click or editing) 显示的保持打开状态（通过双击或编辑）

17:25 默认情况下单击文件打开后其实是一个预览打开的状态，只要不进行编辑或者其他操作的话，当我们再次点击下一个文件时，当前预览文件的编辑区内容会被替换成新的文件，第一次点击的文件并不会在选项卡中占据实际位置，如果你想每次单击打开文件时都想占据实际的选项卡位置的话，可以设置 "workbench.editor.enablePreview": false，但是通过这个设置中给我的注释信息我了解到（下面），可以通过双击文件或者按下快捷键 Command + S 来保持文件打开状态，想想有时候我们的确只是单纯的想预览某些文件而已，所以我更喜欢这种方式。

安装 VSCode Animation 插件，只开启了关于面板和滚动列表的动画，设置为 Fade（淡入淡出效果） 侧边栏的收缩动画模式开启后可能会导致 Vim 在操作移动时出现部分卡顿，所以体验后就选择关闭了。

22:40 VSCode 小技巧：通过呼出系统命令菜单栏输入 Developer: Inspect Editor Tokens and Scopes，可以快速点击 Editor 中的任意关键字看到对应的 textMetaRules 参数，终于不用一个个试了。

07:30 [VS Code When Clause Contexts](https://code.visualstudio.com/api/references/when-clause-contexts)

04:00 本来想找个用于代替 Panda Syntax 的主题，毕竟一直用一个主题也会产生视觉疲劳，在推上翻了好久也没看到满意的，哎 😮‍💨，不过倒是发现了个不错的 file icon：POP! Icon Theme，日常用到的文件类型图标都覆盖到了，样式和 Mac 也比较搭。

14:30 在官方的主题预览网站：[VS Code Themes](https://vscodethemes.com/)，看到了 [Spacegray VSCode](https://github.com/mihai-vlc/spacegray-vscode)，选择的是 Spacegray Eighties Dark 这个风格，比起 Panda 来说，整体配色更扁平化一点（我也不知道怎么形容），反正在白天看着是比 Panda 更舒服的，不过有一些关键字样式没有设置好，比如 JSON 文件中 key 和字符形式的 value 配色是一样的容易让人分不清，不过这个倒是小问题，找到对应关键字改一下就好了。

- 新建文件：Command + N
- 创建无标题文件：Command + T
- 添加针对单个编辑组宽度增加/缩小/恢复的快捷方式：Command + Shift + - / = / 0
- Run Code 快捷键变更为：Command + Option + N

## 小技巧

### 批量删除所有插件

> 导出 extensions.txt 文件

```shell
code --list-extensions > extensions.txt
```

> 通过脚本删除

```shell
# 读取 extension.txt 文件中的插件 ID 到数组
extensions=($(cat extensions.txt))

# 循环遍历数组，逐个删除插件
for extension in "${extensions[@]}"

do
  code --uninstall-extension "$extension"
done
```

## 问题记录

2023-08-28 鼠标 hover 在函数或者输入变量等提示上会出现重复的选项

> 现象

1. 最开始认为肯定是插件的问题，现象也确实如此，通过扩展自带二分查找功能锁定了 `Vue.Volar`，禁用插件后解决问题（但无奈没这个插件写不了 Vue3，问了下群友，让帮忙测试下，发现不能复现这个问题）
2. 切换到了一个纯净的 Profile 环境，这里只安装了 `Vue.Volar` 插件，测试发现确实没有问题
3. 陷入思考：难道是其他某个插件冲突了？于是开始导出了当前配置，复刻了个一模一样的 Profile 环境手动二分查找配置，通过将插件配置文件导入导出的方式每次选择一半，有问题就继续切一半导出导入，测试没有问题就回去选另一半重复操作，大概 6 次左右，所有插件都试过了，还是有问题，此时的我：啊？？？🤨
4. 灵光一闪，突然想到一开始切换的纯净 Profile 环境没有迁移我的 settings 等配置的，于是开始看 settings 配置，终于给爷找到问题了！😭

> 解决方案

- 将 Vue.Volar 从单独配置线程内去掉

2023-08-01 VSCode 中 Vue template 内的 img 标签 src 属性使用别名的方式（配置了 webpack/Vite 别名，以及 tsconfig.json 中的 paths），hover 可以显示图片信息，鼠标点击链接显示资源无法访问，但是放到 script 标签中使用点击访问是可行的，单纯看 VSCode 编辑器内的访问路径其实是错误的，没有额外解析别名映射的路径，是否有其他配置方式能够解决这个问题，如下图：

### VS Code 中关于 CheckJS 导致文件内变量无提示的问题

这个问题给我找麻了，排查了插件，又一个一个排查设置，浪费了好多时间，一开始认为既然是提示问题，那肯定是和关键字 suggest 挂钩，结果相关配置项全看了遍并尝试改值，没啥用，就纳闷了，切换到临时 Profile 测试，诶，没问题。

几经折腾，结果发现是 CheckJS 搞鬼的，不知道什么时候设置的，改成下面这样就好了（其实就是默认设置）

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/VSCode%20CheckJS.png)
