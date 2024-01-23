## fnm

## pm2

本地部署 Next.JS 项目

```shell
pm2 start pnpm --name "earthworm" -- dev
```

`--name` 设置应用名称，`-- dev` 表示通过 `package.json` 中 `script` 的 `dev` 命令启动
