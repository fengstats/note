## 主题截图

![Moegi-Light-Vitesse.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Moegi-Light-Vitesse2.png)

![Github-Dark-Classic.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Github-Dark-Classic2.png)

![Light-Modern.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Light-Modern2.png)

## 小技巧

### 批量删除所有插件

> 导出 extensions.txt 文件

```shell
code --list-extensions > extensions.txt
```

> 通过脚本删除

```shell
# 读取 extension.txt 文件中的插件 ID 到数组
extensions=($(cat extensions.txt))

# 循环遍历数组，逐个删除插件
for extension in "${extensions[@]}"

do
  code --uninstall-extension "$extension"
done
```

## 问题记录

2023-08-28 鼠标 hover 在函数或者输入变量等提示上会出现重复的选项

> 现象

1. 最开始认为肯定是插件的问题，现象也确实如此，通过扩展自带二分查找功能锁定了 `Vue.Volar`，禁用插件后解决问题（但无奈没这个插件写不了 Vue3，问了下群友，让帮忙测试下，发现不能复现这个问题）
2. 切换到了一个纯净的 Profile 环境，这里只安装了 `Vue.Volar` 插件，测试发现确实没有问题
3. 陷入思考：难道是其他某个插件冲突了？于是开始导出了当前配置，复刻了个一模一样的 Profile 环境手动二分查找配置，通过将插件配置文件导入导出的方式每次选择一半，有问题就继续切一半导出导入，测试没有问题就回去选另一半重复操作，大概 6 次左右，所有插件都试过了，还是有问题，此时的我：啊？？？🤨
4. 灵光一闪，突然想到一开始切换的纯净 Profile 环境没有迁移我的 settings 等配置的，于是开始看 settings 配置，终于给爷找到问题了！😭

![image.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20230828165343.png)

![image.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20230828165412.png)

> 解决方案

- 将 Vue.Volar 从单独配置线程内去掉

![image.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20230828165249.png)

2023-08-01 VSCode 中 Vue template 内的 img 标签 src 属性使用别名的方式（配置了 webpack/Vite 别名，以及 tsconfig.json 中的 paths），hover 可以显示图片信息，鼠标点击链接显示资源无法访问，但是放到 script 标签中使用点击访问是可行的，单纯看 VSCode 编辑器内的访问路径其实是错误的，没有额外解析别名映射的路径，是否有其他配置方式能够解决这个问题，如下图：

![image.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/20230801162200.png)
