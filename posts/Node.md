## 国内镜像源

关于 [淘宝镜像域名证书正式过期](https://twitter.com/fengmk2/status/1749276617187221906)

使用旧淘宝镜像源地址 `https://registry.npm.taobao.org/` 需要手动切换到最新的镜像，不然拉取依赖时会报错

```shell
# npm
npm set registry https://registry.npmmirror.com/
# pnpm
pnpm set registry https://registry.npmmirror.com/
```

查看是否设置成功

```shell
npm get registry
pnpm get registry
```

遇到 `pnpm` 报错

```shell
 ERR_PNPM_REGISTRIES_MISMATCH  This modules directory was created using the following registries configuration: {"default":"https://registry.npm.taobao.org/"}. The current configuration is {"default":"https://registry.npmmirror.com/"}. To recreate the modules directory using the new settings, run "pnpm install".
```

尝试下面的命令

```shell
pnpm i -g
# or
pnpm i -g pnpm
# or
npx pnpm i -g pnpm@latest
```

## nrm

一键切换镜像源设置的工具

```shell
# 安装
pnpm i -g nrm

# 查看
nrm ls

# 切换
nrm use tabo
```

## fnm

## pm2

本地部署 Next.JS 项目

```shell
pm2 start pnpm --name "earthworm" -- dev
```

`--name` 设置应用名称，`-- dev` 表示通过 `package.json` 中 `script` 的 `dev` 命令启动
