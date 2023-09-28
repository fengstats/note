## 鼠标点击行末尾光标显示问题

点击当前代码行的末尾（空的地方），它会在末尾多出一个空格然后才回到最后一个字符上

![](attachments/neovim-鼠标点击行末尾问题.mp4)

## 配置 gj 与 gk 映射导致指令不丝滑问题

VSCodeVim 提供了 `"vim.foldfix"; true` 配置，NeoVim 貌似没提供，现在的情况就是遇到折叠代码会自动展开，配置 gj&gk 可以解决（这应该算另一个问题了，不管了，先放在这），但是会导致使用流畅度大大下滑，而且不能完全解决（在 VISUAL 模式无效），比如在重复执行 je je je 时能够直观的看到，e 指令会慢一点，导致 e 接收到的是上次的位置，就这样卡着一直重复在同一个位置执行（预期结果应该是一直往下走的才对），不知道是不是内部实现问题，在我看来不就多了一个 g 指令呀，不至于吧

折叠问题，通过配置 `map J 4gj` 临时解决

![](attachments/neovim-gj与gk导致指令不丝滑问题.mp4)

## VISUAL LINE 影响鼠标选中问题

按 V 进入 visual line（行选中模式）选择几行代码进行操作， 结束后按 esc 回到 normal 模式，那么后续在 normal 模式下使用鼠标进行区域选中时会自动变成 visual line 而不是 visual，比如：你选中一行的开头或者中间，它会自动帮你选中整行，如何解决？

1. 先把 visual line 变成 visual，也就是按 v，然后按 esc 退出，此时再用鼠标选中就没问题了
2. 重新加载 VS Code

![](attachments/neovim-visualline影响鼠标选中问题.mp4)

## Command+D 无法在 Normal 模式创建多光标选中操作

如题，临时解决方案是通过进入 Insert 模式操作