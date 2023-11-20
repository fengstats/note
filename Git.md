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
