## 前言

第一个 PR！开心 😊

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/GitHub%20%E6%88%91%E7%9A%84%E7%AC%AC%E4%B8%80%E4%B8%AA%20PR.png)

## 小问题收集

关于我更改 GitHub 仓库名后，没有改本地 remote 名称同样可以 push 的原因，参考文档：[GitHub 文档](https://docs.github.com/zh/repositories/creating-and-managing-repositories/renaming-a-repository)

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
