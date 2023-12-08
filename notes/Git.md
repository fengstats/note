重命名分支 -M 表示强制重命名，即使新分支存在也会执行重命名。

git branch -M main

将当前分支推送到远程仓库，-u 将远程仓库和 main 分支进行关联，下次直接 git push 即可。

git push -u origin main

这里的 `--depth=1` 意思是只克隆最近一次提交，而不是克隆整个提交历史，可以减少克隆的时间，因为我们只需要最新的代码。

`gitignore` 的问题直接 `git rm --cached` 清除之后 `add + commit` 解除远程仓库托管即可（也就是删除远程上的文件），记得要加上 `--cached` 不然本地的文件也会被删除。

## 子模块

- [Git 子模块](https://git-scm.com/book/zh/v2/Git-%E5%B7%A5%E5%85%B7-%E5%AD%90%E6%A8%A1%E5%9D%97) - 通过 `git submodule` 链接一个独立的子仓库进行管理

> 创建一个子模块

```shell
git submodule add 远程仓库地址
```

> 更新主项目中子模块的引用

```shell
git submodule update --remote
```

**更新前请务必要确保子模块仓库没有未提交的更改！！！😭**

> 如果需更改子模块，一下配置需要同步更新：

- `.git/config` 配置
- `.gitmodules` 映射
- `.git/modules/` 目录下无用子模块清理
