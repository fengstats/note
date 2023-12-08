01:50 之前网页版抖音弹幕不显示问题，居然随便发一个弹幕就有了，真不知道这个东西是怎么设计的，无语 💬。

> 力扣

关于力扣不能正常登录的情况，中国区的先确认正确的帐号密码，帐号是手机号和邮箱，不能用 github 名称来登录，确认没问题可以试试 Cookie 登录，拿到 Cookie key 为 csrftoken 的值，如果都不行，那把网站上的帐号退出，登录插件的试试。

22:15 浏览器重装的一些注意事项：无法恢复数据的扩插件一定要备份好，比如油猴、身份验证器、stylish 等等，哎，为了清一个地址栏搜索记录列表搞的有点烦了，早知道就不弄了，靠。

油猴本身提供了备份选项，但我之前没弄，所以现在什么脚本都没了，重新弄吧，索性这次把 tamlermonkey 换成 violentmonkey，后者是根据前者闭源前改的，据说同步功能也挺好用的，这次试试（暴力猴界面简洁好看，同时也可以设置 Google Drive 同步）。

Stylish 就更离谱了，我明明在它上面登录了 Google 帐号保存居然也没了？？？真的坑。

Chrome 自定义主题颜色的小坑，昨天找到个挺喜欢的自定义颜色用了一天，因为一直在弄这个地址栏，反复卸载了 Chrome N 次把我都搞烦了，期间浏览器更新了一下，更新后的新版取色条只能用滑块形式没法自定义了，我手贱点了一个恢复默认，哦吼，这下这个颜色回不去了，所以只能卸载找了个低版本，先利用原版取色条取自定义颜色然后通过 google 帐号来同步这个主题颜色，又是一波曲线救国，我真服辣！

00:35 参考仓库 Issues 答复：[Request command to toggle "Disable for once" #113](https://github.com/gdh1995/vimium-c/issues/113#issuecomment-580055009)

> Vimium C Options 配置命令如下：

```vim
map Z openUrl url="vimium://status toggle ^ Z"
```

### Chrome

> [!question] 在 Google 搜索页或者 Github 网页中点击一些链接，默认是在当前网页打开的，这会使前面浏览的内容被覆盖，如果想在新标签页打开并且自动跳到此标签页该怎么办呢？
>
> 点击链接时加上两个修试键：Command + Shift

> [!tip] 控制台快捷键
>
> - 全局命令面板：Command + Shift + P
> - 全局文件面板：Command + P
> - 切换上一个 panel（面板）：Command + [
> - 切换下一个 panel（面板）：Command + ]
> - 在其他的面板调出一个临时控制台（可通过 Esc 隐藏）：Ctrl + `
> - 控制台清屏：Command + K

### Chrome 显示右上角的下载按扭

要开启实验性功能（咱不知道微软怎么想的，这种功能不正式发版出来，还要用户去找）

- 访问 chrome://flags/#download-bubble 将默认的 Default 改为 Enabled，然后按提示重启浏览器即可

接下来，当你开始进行下载任务时，Chrome 底部的下载栏将不会再出现，取而代之的是右上角的下载管理按钮。点击下载按钮可展开管理器，以查看/暂停/取消最近的下载任务。

### Chrome

19:55 Chrome 控制台的一个小技巧，让提示建议选项自动聚焦第一个，根据英文解释应该是将补全建议写入 Enter（回车），默认不聚焦情况需要按 Tab 才能补全，我就是 Enter 来补全习惯了，每次按 Enter 时就直接回车执行了，这让我很不爽，想想 VSCode 是有这个配置项的，Chrome 应该也有，还真找到了！

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Chrome%20%E6%8E%A7%E5%88%B6%E5%8F%B0%E8%87%AA%E5%8A%A8%E8%81%9A%E7%84%A6%E5%BB%BA%E8%AE%AE%E6%8F%90%E7%A4%BA%E5%B9%B6%E5%8F%AF%E4%BB%A5%E5%9B%9E%E8%BD%A6%E8%A1%A5%E5%85%A8.png)
