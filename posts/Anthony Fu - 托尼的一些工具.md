## Shikiji 式辞 - 基于 TextMate 的语法高亮

[项目地址](https://github.com/antfu/shikiji)

### 用法

Shikiji CLI 的工作方式和 `cat` 命令类似，但具有语法突出显示功能，如：

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Shikiji%20%E5%92%8C%20cat%20%E5%AF%B9%E6%AF%94%E5%9B%BE.png)

### 安装

可以全局安装 `shikiji-cli`，内部已经注册别名 `shikiji-cli`、`shikiji`、`skat` 以供使用。

```shell
pnpm i -g shikiji-cli

skat src/index.ts
```

### 参数

#### `--theme`

选择主题 [Themes](https://shikiji.netlify.app/themes)，默认主题为 `vitesse-dark`，可以通过 `--theme` 指定其他主题。

```shell
skat index.ts --theme=nord
```

#### `--lang`

选择语言：[Languages](https://shikiji.netlify.app/languages)，一般是由文件扩展名自动推断而来，可以通过 `--lang` 进行覆盖。

```shell
skat index.js --lang=ts
```

## 🥦 Taze - 更现代化的更新依赖工具

[项目地址](https://github.com/antfu/taze)

> [!todo]

## ni - 正确的使用包管理工具

[项目地址](https://github.com/antfu/ni)

### 全局安装

```shell
pnpm i -g @antfu/ni
```

### 安装项目依赖

```shell
ni

# 等于下面命令的其中一个，根据 lockfile 来判断你使用的是哪一个，如果没有则可让用户手动选择
npm install
yarn install
pnpm install
bun install
```

![image.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20230728181542.png)

### 启动项目命令

```shell
nr
```

读取 package.json 中的 scripts 来让用户选择，通过 [npm-scripts-info](https://www.npmjs.com/package/npm-scripts-info) 包实现

![image.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20230728181925.png)

可以在后面追加 scripts 中的命令以及其他指令

```shell
nr dev --port 3000

# 等于下面命令的其中一个
npm run dev -- --port=3000
yarn run dev --port=3000
pnpm run dev --port=3000
bun run dev --port=3000
```

重复最后一次执行的 nr 命令，类似 cd -

```shell
nr -
```

### 临时下载并执行

```shell
nlx

# 如下
npx
yarn dlx
pnpm dlx
bunx
```

### 升级

```shell
nu

# bun 无法使用这个命令
npm upgrade
yarn upgrade # Yarn 1
yarn up # Yarn Berry（较新的版本）
pnpm update
```

```shell
nu -i

# npm 和 bun 无法使用这个命令
yarn upgrade-interactive # Yarn 1
yarn up -i # Yarn Berry
pnpm update -i
```

### 卸载

```shell
nun

# 如下
npm uninstall
yarn remove
pnpm remove
bun remove
```

全局卸载

```shell
nun -g

# 如下
npm uninstall -g
yarn global remove
pnpm remove -g
bun remove -g
```
