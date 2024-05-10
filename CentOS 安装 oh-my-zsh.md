通过 yum 查看某个包的可用版本

```bash
yum --showduplicates list [package-name]

# 示例
yum --showduplicates list zsh
```

挖矿程序，直接 kill -9 掉

![](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/20240422205051.png)

安装 zsh

```bash
sudo yum update && sudo yum -y install zsh
```

检查 zsh 是否存在

![1713619617692.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1713619617692.png)

设置 zsh 为默认 shell

```bash
chsh -s /bin/zsh
```

提示需要安装 Git

![1713619716687.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1713619716687.png)

通过 wget 下载 oh-my-zsh（找个空闲目录，别在根目录操作）

```bash
# 下载 oh-my-zsh 安装脚本
wget https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh

# 安装（注意这个操作会把 .zshrc 文件内容覆盖，如果有很多配置信息记得备份）
sh install.sh
```

然后看到你的终端变成啦这样就搞定啦~ 🎉

![1713713463888.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1713713463888.png)

> 一些插件

autojump 目录快速跳转

```bash
yum install autojump
```

```bash
curl -sS https://raw.githubusercontent.com/ajeetdsouza/zoxide/main/install.sh | bash
```

TODO 配置 `.zshrc` plugin

```bash
plugins+=()
```

## 遇到的一些问题

zsh-vi-mode 脚本解析的问题

![1713790984645.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1713790984645.png)

## 安装 Git

删除旧版本 git

```bash
yum remove git
```

从 [Git](https://git-scm.com/download/linux) 中下载压缩包，按顺序执行下面的命令

```bash
# 解压
tar -zxvf git-2.44.0.tar.gz

# 进入目录
cd git-2.44.0.tar.gz

# 编译
make prefix=/usr/local/git all

# 编译过程中遇到缺少的 C 库
sudo yum install libcurl-devel
sudo yum install expat-devel

# 安装！！！
make prefix=/usr/local/git install
```

配置 `~/.zshrc` 环境变量

```bash
# 写入环境变量配置到 PATH
echo "export PATH=/usr/local/git/bin:$PATH" >> ~/.zshrc

# 重新加载配置
source ~/.zshrc
```

检查是否可以连接 GitHub，

![1713694791392.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1713694791392.png)

如果没有权限则执行

```bash
ssh-keygen -t rsa -C [邮箱]

# 示例
ssh-keygen -t rsa -C "feng2860984180@163.com"
```

将 `id_rsa.pub` 内容添加到 [GitHub SSH keys](https://github.com/settings/keys)

```bash
cat ~/.ssh/id_rsa.pub
```

## 安装 Vim

删除旧版 Vim

```bash
yum remove vim
```

通过源码安装最新版本

```bash
git clone https://github.com/vim/vim.git
cd vim
```

配置编译安装

```bash
./configure

# 编译时缺少的库
sudo 

ncurses-devel

make

make install
```

安装 vim-plug（Vim 必备）

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

在 `.vimrc` 命令模式输入

```bash
# 安装插件
:PlugInstall
```
