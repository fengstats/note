17:30 目前的光标方向移动方案：没有 Vim 的地方，用的是 Karabiner Elements 软件配置 Control + hjkl 快捷键映射方向键，不过按键记忆对不熟悉 Vim 的人挺不友好的，不是很推荐。

12:50 Vim tips：多思考用最少的按键实现你需求，久而久之就转化为肌肉记忆了

> [!tip]
>
> - 可视化模式下 `o` 可以切换光标的位置，比如你从当前位置开始向下选择了 3 行文本，突然发现最上面一行文本也需要选中，这时候按下一个 `o` 光标会回到第一行，再加上一个 `k` 即可选中，如果想回到最后一行选中文本继续向下，再按一个 `o` 即可返回
> - gv：执行上一次的选中操作
> - gd：查看函数定义位置跳转
> - Vim 调用 VS Code 命令时可以写多个 commands: [{command: ""}, …]

> [!note]
>
> - 使用 `:jumps` 查看所有保存的跳转记录
> - 宏：使用 `qa` 来录制宏，录制好后使用 `q` 来结束录制，`@a` 来调用宏，可以通过 `:reg a` 来查看宏，`@@` 执行最后一次录制的宏，@+A 追加宏内容（注意这里的 a 可以是任意字母）

00:55 发现一个问题，VS Code 配置了光标动画之后，Vim 移动如果用的不是 gj/gk 命令，会出现光标拖影，现象就是在一直按 j/k/J/K 时，光标动画会追不上当前行背景高亮，显得有点卡顿

Vim 的数值降序插入，其实想到思路其实很快就弄出来了，但是单个数字比两个数字要多了一个空格，一直在纠结这个问题，不纠结了，手动进入块选择状态删掉好了。发现如果把右边的大括号放到最后添加就不会有这个问题了，比较麻烦的是需要进入好几次块选择的模式（感觉好像也差不太多）

## 使用技巧

### 数值处理

#### 快捷键

> [!note] 传统 Vim 与 Obsidian 中的 Vim 可用，VSCode Vim 不可用（有可能是快捷键配置问题屏蔽了，后面来看）
>
> 补充说明：确实是 VS Code 中快捷键屏蔽问题，不过需要手动开启。
> 再补一个：是我的问题，VS Code 中这个配置项默认就是开启的，我给关闭了……

- 数字自增：Ctrl + A
- 数字自减：Ctrl + X

#### 使用 put 和 range 来快速生成数字

> 只有传统 vim 可用

在所在行的下一行开始，生成 0-4 的数字

```vim
:put=range(5)
```

输出：

```text
0
1
2
3
4
```

你也可以通过一些变量来控制排序以及步长，比如：

生成 1-10 之间的奇数（升序，包括 1）：

```vim
:put=range(1,10,2)
```

输出：

```text
1
3
5
7
9
```

生成 10-1 之间的偶数（降序，包括 10）：

```vim
:put=range(10,1,-2)
```

```text
10
8
6
4
2
```

#### 快速增加已有数字列的值

三步即可，如下：

- 第一步：创建五个「这是任务 0」
- 第二步：光标移动到第一个 0 上，通过 Ctrl + V 进入 V-BLOCK 模式，向下选择其他的 0
- 第三步：先按下字母 `g`，然后按下快捷键 Ctrl + A，怎样？是不是很神奇 😙

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Vim-%E5%BF%AB%E9%80%9F%E5%A2%9E%E5%8A%A0%E6%95%B0%E5%AD%97%E5%BA%8F%E5%88%97%E5%80%BC.png)

#### 在行内指定位置添加数字列

> 感觉有点麻烦，算是扩展下知识吧，原理也还是通过找匹配项的操作实现的，那有可能某些行没有这个通用的匹配项不就匹配不到了，不如先进入 V-BLOCK 在后面添加一个 0 或者你想要开始递增的数值，然后使用上面的第三种方式一下就搞定了

命令：

```vim
:'<,'>s/{这是个变量，你想要匹配什么就填什么}\zs\d*\ze/\=line(".")-line("'<") + 1
```

> TODO: 下面是别人的解析描述，有时间仔细看下，现在没兴趣，能用就行

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2023/Vim-%E6%95%B0%E5%AD%97%E5%BA%8F%E5%88%97%E5%91%BD%E4%BB%A4%E8%A7%A3%E6%9E%90.png)