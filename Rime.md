## Mac 获取 squirrel.custom.yaml 中的 app_options

把 `Raycast.app` 更换为其他你想要获取应用的名称即可

```shell
grep -A 1 "CFBundleIdentifier" /Applications/Raycast.app/Contents/Info.plist
```

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/grep%20%E8%8E%B7%E5%8F%96%20Mac%20%E5%BA%94%E7%94%A8%20app_options.png)

图中框选的 `com.raycast.macos` 就是你想要的值

## 关于配色的问题

服辣！Rime 配置的 16 进制配色和正常的 16 进制配色对不上，更像是互补色，只有在这里设置的才是准确的：[Rime 西米](https://fxliang.github.io/RimeSeeMe/)

## 解决 VSCode 新建终端快捷键冲突问题

> 解决 Control + \` 冲突问题，参考文档：[定制呼出方案的快捷键](https://github.com/rime/home/wiki/CustomizationGuide#%E4%B8%80%E4%BE%8B%E5%AE%9A%E8%A3%BD%E5%96%9A%E5%87%BA%E6%96%B9%E6%A1%88%E9%81%B8%E5%96%AE%E7%9A%84%E5%BF%AB%E6%8D%B7%E9%8D%B5)

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Rime-%E5%88%87%E6%8D%A2%E6%96%B9%E6%A1%88%E5%BF%AB%E6%8D%B7%E9%94%AE.png)

## iCloud 同步目录

> 参考文档：[Rime Squirrel 鼠须管输入法配置详解](https://ssnhd.com/2022/01/06/rime)

1. 打开 Rime 的配置目录，找到 `installation.yaml` 文件
2. 添加参数 `sync_dir`，把 `feng` 替换成你自己的管理员名称即可
3. 更改参数 `installation_id`，随意即可（后续同步的目录名称）
4. 点击 重新部署
5. 打开 iCloud 查看是否同步成功

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Rime-%E5%90%8C%E6%AD%A5%20iCloud.png)
