## 基础

### 用户

清除用户名与邮箱命令（全局）

```bash
git config --global --unset user.name
git config --global --unset user.email
```

设置用户名与邮箱命令（全局）

```bash
git config --global user.name "用户名"
git config --global user.email "邮箱"
```

查看用户名邮箱（全局）

```bash
git config --global --list
```

Windows 下保存 Gitee 账号密码路径

```
控制面板 → 用户帐户 → 凭据管理器 → 找到 https://gitee.com
```

### 分支

创建分支

```bash
git branch branch-name

# 创建空分支
git checkout --orphan main
```

切换分支

```bash
git checkout branch-name
```

创建并切换分支

```bash
git chekout -b branch-name
```

删除分支

```bash
git branch -d branch-name
```

删除远程分支

```bash
git push origin :branch-name
```

### 保存工作进度并在需要的时候恢复

会分别对 **暂存区** 和 **工作区** 的文件进行进度保存

```bash
git stash

# 完整版本
git stash save "message…"
```

如果你想要将 **新添加的文件** 也保存起来

```bash
git stash -u
# or
git stash --all
```

在你需要的时候可以将进度弹出对文件进行恢复

```bash
git stash pop
```

查看保存的进度

```bash
git stash list
```

清空暂存区

⚠️ 这将清空整个 stash 列表，删除所有存储的更改，在执行删除操作之前，请确保你确实不再需要这些存储的更改，因为一旦删除，它们将无法恢复。如果你不确定，可以先使用  `git stash apply`  或  `git stash pop`  来恢复更改，检查是否还需要这些更改，然后再决定是否删除。

```bash
git stash clear
```

### 克隆最新提交的仓库并重命名

这里的 `--depth=1` 意思是只克隆最近一次提交，而不是克隆整个提交历史，可以减少克隆的时间，因为我们只需要最新的代码。

```bash
# 这里用的是 plum 举例，在 git 地址后可以加上想要的项目名称
git clone --depth=1 https://github.com/rime/plum  my-plum
```

### 强制重命名分支

-M 表示强制重命名，即便新分支存在也会执行重命名。

```bash
git branch -M main
```

### 推送分支并和远程仓库关联

将当前分支推送到远程仓库，通过 `-u` 关联远程仓库和 main 分支，后续使用 `git push` 即可。

```bash
git push -u origin main
```

## 出现冲突怎么办

如果你想要使用合并（merge）来解决冲突，可以执行

```bash
git config pull.rebase false
```

如果你想要使用变基（rebase）来解决冲突，可以运行

```bash
git config pull.rebase true
```

`git merge` 到一半不想解决冲突了怎么办？

```bash
# 这将会取消合并，并且将代码状态恢复到合并之前的状态
git merge --abort
```

## 中文显示转义乱码

> 如图所示：

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Git%20%E4%B8%AD%E6%96%87%E6%98%BE%E7%A4%BA%E8%BD%AC%E4%B9%89%E4%B9%B1%E7%A0%81.png)

执行下面命令关闭对文件名的 quote 即可

```bash
git config --global core.quotepath false
```

## 更改 commit 提交时间（不建议多人合作项目使用）

找到需要更改信息的 commit 哈希值

```bash
git rebase -i commitHash~1
```

将 `YYYY-MM-DD HH:MM:SS` 更改成你想要的时间

```bash
GIT_COMMITTER_DATE="YYYY-MM-DD HH:MM:SS" git commit --amend --no-edit --date "YYYY-MM-DD HH:MM:SS"
```

结束

```bash
git rebase --continue
```

强制提交

```bash
git push --force
```

## commit msg 已提交如何修改？

⚠️ 多人协作可能要考虑一下后果

1. 查看需要修改 commit 信息的 hash 值

```bash
git log
git reflog
```

2. 找到此 commit 的位置的父 commit hash 信息 ~ 后面的代表回数几个 commit

```bash
git rebase -i commitHash~1
```

3. 进入 Vim 编辑，找到你需要修改的 commit msg 行，将前面的 `pick` 更改为 `reword` 或 `r`，Vim `:x`，保存并退出
4. 此时会自动弹出这个 commit msg 之前的提交信息，对其进行修改并保存退出
5. 强制提交

```bash
git push --force
```

## gitignore 怎么忽略已提交的文件

> ⚠️ 要加上 **--cached**，否则本地的文件也会被删除。

1. 先 `git rm --cached` 清除这个文件或文件夹；
2. `git add` 加上 `git commit` 清除远程仓库托管信息即可，也就是删除远程仓库的文件或者文件夹。

## submodule 子模块

[sumodule](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E5%9D%97) - 链接一个独立的子仓库进行管理。

### 创建

```bash
git submodule add 远程仓库地址
```

### 更新主项目中子模块的引用

```bash
git submodule update --remote
```

⚠️ **更新前请务必要确保子模块仓库没有未提交的更改！！！😭**

> 修改子模块，以下配置需要同步更新：

- `.git/config` 配置
- `.gitmodules` 映射
- `.git/modules/` 目录下无用子模块清理

## 文件名大小写所产生的问题

例如：你创建了一个文件 `callout.md` 写入内容并提交到远程仓库中，突然有一天，你想将这个文件名的首字母改为大写，更改后会发现没有任何提示信息，你感到很诧异，这并不奇怪，因为 Git 默认是不区分文件名大小写的，所以对你的文件名大小写并不敏感。

> 那么我们怎么能让 Git 对大小写敏感呢？很简单，一个命令：

```bash
git config core.ignorecase false
```

执行完命令之后，不出意外的话你会发现 Git 仓库有文件的修改信息提示了，于是你兴冲冲的将 `add&commit&push` 一套组合拳打在 Git 身上，但这可能仅仅是个开始…你打开 Git 远程仓库一看，诶！怎么有两个文件？🤨 一个是首字母大写的 `Callout.md`（修改后），一个是没大写的 `callout.md`（修改前），明明你的本地只有一个啊

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Git-%E6%96%87%E4%BB%B6%E5%A4%A7%E5%B0%8F%E5%86%99%E7%9B%AE%E5%BD%95.png)

小问题，不要慌 👊，清除一下本地 Git 记录的文件缓存信息，然后重新提交即可，如下：

```bash
# -r 是为了递归删除，多个文件的话，建议你直接写目录名，反正在 add 阶段会被 Git diff 掉
# !!! 注意一定要加上 --cached 选项，如果不加，不仅会删除托管信息，还会在硬盘上删除此文件
git rm -r --cached callout.md

git add callout.md
git commit -m "chore: rm cached file"
git push
```

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Git-%E6%96%87%E4%BB%B6%E5%A4%A7%E5%B0%8F%E5%86%99%E8%A7%A3%E5%86%B3%E6%B5%81%E7%A8%8B%E6%BC%94%E7%A4%BA.png)
