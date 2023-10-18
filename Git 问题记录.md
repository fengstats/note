## 更改已提交的 commit msg 信息

1. `git log` 或者 `git reflog` 查看 commit hash 值。
2. `git rebase -i commitHash~1`
3. 在 Vim 编辑内容中，找到你想要更改 commit msg 信息的行，将前面的 `pick` 更改为 `reword` 或 `r`
4. 保存退出，此时会自动弹出当时的 commit msg，修改保存退出
5. 强制提交，`git push --force`

## 文件名大小写

例如：你创建了一个文件 `callout.md` 写入内容并提交到远程仓库中，突然有一天，你想将这个文件名的首字母改为大写，更改后会发现没有任何提示信息，你感到很诧异，这并不奇怪，因为 Git 默认是不区分文件名大小写的，所以对你的文件名大小写并不敏感。

> 那么我们怎么能让 Git 对大小写敏感呢？很简单，一个命令：

```shell
git config core.ignorecase false
```

执行完命令之后，不出意外的话你会发现 Git 仓库有文件的修改信息提示了，于是你兴冲冲的将 `add&commit&push` 一套组合拳打在 Git 身上，但这可能仅仅是个开始…你打开 Git 远程仓库一看，诶！怎么有两个文件？🤨 一个是首字母大写的 `Callout.md`（修改后），一个是没大写的 `callout.md`（修改前），明明你的本地只有一个啊

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Git-%E6%96%87%E4%BB%B6%E5%A4%A7%E5%B0%8F%E5%86%99%E7%9B%AE%E5%BD%95.png)

小问题，不要慌 👊，清除一下本地 Git 记录的文件缓存信息，然后重新提交即可，如下：

```shell
# -r 是为了递归删除，多个文件的话，建议你直接写目录名，反正在 add 阶段会被 Git diff 掉
# !!! 注意一定要加上 --cached 选项，如果不加，不仅会删除托管信息，还会在硬盘上删除此文件
git rm -r --cached callout.md

git add callout.md
git commit -m "chore: rm cached file"
git push
```

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Git-%E6%96%87%E4%BB%B6%E5%A4%A7%E5%B0%8F%E5%86%99%E8%A7%A3%E5%86%B3%E6%B5%81%E7%A8%8B%E6%BC%94%E7%A4%BA.png)

## gitignore 忽略已经提交过的文件

> 记得要加上 `--cached` 不然本地的文件也会被删除。

1. 先 `git rm --cached` 清除这个文件或文件夹
2. `add + commit` 解除远程仓库托管即可（也就是删除远程上的文件）
