## 前言

第一个 PR！开心 😊

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/GitHub%20%E6%88%91%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%20PR.png)

## 小问题收集

### 在 push 一个分支后，仓库页面的 “合并 & 拉取请求” 提示框如何关闭？

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/GitHub%20%E5%90%88%E5%B9%B6%E6%8B%89%E5%8F%96%E8%AF%B7%E6%B1%82%E6%8F%90%E7%A4%BA%E6%A1%86.png)

emm……就不用管，超过一个小时会自动消失的。

### 更改仓库名后你需要知道的一切

1. 之前的仓库链接同样可以正常访问
2. 本地 remote 地址没有更新的情况下也可以 push 的原因

参考文档：[GitHub 文档](https://docs.github.com/zh/repositories/creating-and-managing-repositories/renaming-a-repository)

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/GitHub%20%E9%87%8D%E5%91%BD%E5%90%8D%E4%BB%93%E5%BA%93%E6%96%87%E6%A1%A3.png)

## 如何提交一个 Pull Request

### 一、找到你想提交 PR 的仓库，点击 Fork

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/GitHub%20fork%20repository.png)

### 二、将 Fork 后的仓库 Clone 到本地（注意是自己的仓库）

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/GitHub%20fork%20clone.png)

### 三、创建一个新的分支用于解决某个问题的 PR 提交

在此分支进行代码功能更新，可以提交多个 `commit msg`，建议细分功能提交

分支名称应该见名知意，比如 `feat/xxx`、`fix/xxx`

```shell
git checkout -b feat/add-feature
```

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/Git%20%E5%88%9B%E5%BB%BA%E5%88%86%E6%94%AF%E6%8F%90%E4%BA%A4%E4%BB%A3%E7%A0%81%E7%A4%BA%E8%8C%83.png)

> ⚠️ 尽量不要在主分支 `main` 上做 PR 提交

只在 `main` 分支提交会导致在这个 PR 被合并后，下次 PR 时，你的 `commit msg` 会留存上次 PR 的信息，就不干净了，而创建一个新分支的方式能很好的解决这个问题，`main` 分支主要作用就是同步 `Fork` 前仓库

### 四、将此分支 push 到你的仓库

```shell
git push origin feat/add-feature
```

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/Git%20branch%20push.png)

### 五、提交 PR 到原 Fork 仓库指定分支

回到 `Fork` 的仓库时，首页会出现提示，点击 **Compare & pull request**

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/GitHub%20%E6%AF%94%E8%BE%83%E6%88%96%E6%8F%90%E4%BA%A4%E8%AF%B7%E6%B1%82.png)

来到这个页面将这个 PR 所解决的问题写在 **Add a description** 中，并将核心内容概括取一个好一点的 **title**，更有利于维护者来快速了解并 review 你的代码

确认好了点击 **Create pull request**

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/GitHub%20PR%20%E9%A1%B5%E9%9D%A2%E4%BF%A1%E6%81%AF.png)

### 六、等待仓库维护者合并 PR

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/GitHub%20%E7%AD%89%E5%BE%85%20PR%20%E5%90%88%E5%B9%B6.png)

## 关于两个没有权限的 GitHub 用户合作一个 PR 的问题

### 基础步骤

1. 先 fork 原仓库（你们都想要把 pr 提交过去的仓库）
2. 决定谁来提 PR（A），谁作为合作者（B）
3. A 提交一个 PR 之后，在他 fork 的仓库中将 B 添加到合作者（collaborator）
4. B 在他 fork 的仓库找到 A 提交的 PR 分支，并且切换（checkout）过去
5. 基于这个 PR 分支的内容进行添加 / 更改 / 删除之后，push 到他的分支上（此时是有权限的）

### 纯命令行形式

> 确保本地是干净的，可以先用 git stash 存起来，等你改完之后再 git stash pop 出来

切换分支

```bash
# username 是对方的
git checkout pr/[username]/[prId]

# 比如
git checkout pr/fengstats/1
```

添加暂存区 + 提交本地仓库

```bash
git add .
git commit -m "xxx"
```

推送到 PR 分支上（确保有其仓库推送的权限 / Collaborator）

```bash
git push [username] HEAD:对应的分支名称

# 比如
git push fengstats HEAD:feat/add-content
```

### 图形化方式

推荐 VSCode 插件：[GitHub Pull Requests](https://marketplace.visualstudio.com/items?itemName=GitHub.vscode-pull-request-github)

![1712158228477.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/VSCode%20GitHub%20Pull%20Requests.png)

切换到对应 PR 的分支上

![1712158271074.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/VSCode%20GitHub%20Pull.png)

通过 add&commit 提交到本地仓库之后，会看到一个分支差异，右键推送即可

![1712158367467.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1712158367467.png)
