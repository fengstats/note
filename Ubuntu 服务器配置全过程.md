## crontab 定时任务

- /etc/crontab
- /var/spool/cron：用户定义的 crontab 文件存放目录
- /etc/cron.d：存放要执行的 crontab 文件或脚本
- /etc/crontab：系统任务调度的配置文件
- /etc/anacrontab：anacron 配置文件
- /etc/cron.deny：列出不允许使用 crontab 命令的用户
- /etc/cron.daily：每天执行一次的脚本
- /etc/cron.hourly：每小时执行一次的脚本
- /etc/cron.monthly：每月执行一次的脚本
- /etc/cron.weekly：每星期执行一次的脚本

## ssh 免密登录 ✅

命令

```bash
ssh-keygen -R [serve-ip]
ssh-copy-id [username]@[serve-ip]
ssh [username]@[serve-ip]
```

示例

```bash
# 生成服务器密钥
ssh-keygen -R 121.4.83.62

# 上传服务器密钥
ssh-copy-id ubuntu@121.4.83.62

# 登录服务器
ssh ubuntu@121.4.83.62
```

## ubuntu 的 root ✅

默认关闭，需要自己开启 root 登录，一般在需要执行命令的前面添加 `sudo` 指令即可

```bash
# 提升到 root 权限执行命令
sudo xxx

# 新开 shell 保持 root 权限，直到你退出为止
sudo -i

# 设置 root 用户密码 + 切换
sudo passwd root
su - root
```

更新 ssh 配置来允许 root 用户登录（root 下操作）

```bash
vim /etc/ssh/sshd_config

# 找到下面的参数，设置为
PermitRootLogin yes

# 退出到命令输入界面，重启 ssh 服务
systemctl restart sshd
```

设置终端保持连接时长（root 下操作）

因为 ssh 连接到服务器一段时间之后不操作后会自动退出，无法操作

- ClientAliveInterval 代表服务端多久向客户端发一次包确认连接
- ClientAliveCountMax 代表需要发多少次确认

```bash
vim /etc/ssh/sshd_config

# 添加 或 更改下面两个值
ClientAliveInterval 60
ClientAliveMaxCount 60
```

## git ✅

[GitHub Proxy 代理加速](https://gh-proxy.com/)

在 clone 和下载的时候配置代理

```bash
git clone https://gh-proxy.com/https://github.com/[xxx]
```

## 配置 git ssh ✅

检查是否可以访问

```bash
ssh -T git@github.com
```

没有权限的情况

![1713875259580.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1713875259580.png)

执行下面的命令

```bash
ssh-keygen -t rsa -C [邮箱]

# 示例
ssh-keygen -t rsa -C "feng2860984180@163.com"
```

将 id_rsa.pub 文件内容添加到 [GitHub SSH keys](https://github.com/settings/keys)，执行

```bash
cat ~/.ssh/id_rsa.pub
```

再次检查，下图代表配置成功

![1713875583355.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1713875583355.png)

## 1 panel ✅

- [1Panel - 现代化、开源的 Linux 服务器运维管理面板](https://1panel.cn/)
- [GitHub - 1Panel-dev/1Panel: 🔥 🔥 🔥 现代化、开源的 Linux 服务器运维管理面板。](https://github.com/1Panel-dev/1Panel)

## docker ✅

装 panel 的时候带上了

## vim + plug.vim ✅

[vim-plug](https://github.com/junegunn/vim-plug)

```bash
curl -fLo ~/.vim/autoload/plug.vim --create-dirs https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim
```

## zsh ✅

```bash
apt install zsh
```

配置 alias

```bash
# 刷新 zsh 配置后 / 进入一个新的 zsh 会话，避免配置没更新的问题
alias so="source ~/.zshrc && exec zsh"
```

## oh-my-zsh ✅

```bash
sh -c "$(curl -fsSL https://gh-proxy.com/https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## oh-my-zsh plugin ✅

[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions/) 命令补全提示 ✅

```bash
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```

[zsh-vi-mode](https://github.com/jeffreytse/zsh-vi-mode) 命令行的 vim ✅

```bash
git clone https://github.com/jeffreytse/zsh-vi-mode \
  $ZSH_CUSTOM/plugins/zsh-vi-mode
```

[autojump](https://github.com/wting/autojump) 快速跳转目录 ✅

```bash
git clone https://gh-proxy.com/https://github.com/wting/autojump.git
```

进入目录并执行安装脚本

```bash
cd autojump
./install.py
```

执行结果如图所示

![1713949649795.png](https://cdn.jsdelivr.net/gh/fengstats/blogcdn@main/2024/1713949649795.png)

[zsh-syntax-highlighting](https://github.com/zsh-users/zsh-syntax-highlighting) 关键字高亮

```bash
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

[zsh-completions](https://github.com/zsh-users/zsh-completions) 命令补全

```bash
git clone https://github.com/zsh-users/zsh-completions ${ZSH_CUSTOM:-${ZSH:-~/.oh-my-zsh}/custom}/plugins/zsh-completions
```

配置 `.zshrc`

```bash
# ===================== alias =====================
alias so="source ~/.zshrc && exec zsh"

# ===================== zsh-vi-mode =====================
KEYTIMEOUT=50

bindkey -M vicmd "H" vi-beginning-of-line
bindkey -M vicmd "L" vi-end-of-line

# ===================== autojump =====================
[[ -s /root/.autojump/etc/profile.d/autojump.sh ]] && source /root/.autojump/etc/profile.d/autojump.sh
autoload -U compinit && compinit -u

# ===================== plugins =====================
plugins=(
  git
  zsh-autosuggestions
  zsh-vi-mode
  zsh-syntax-highlighting
  zsh-completions
)
```

## 本地域名访问 ✅

直接暴露 IP 的方式难免会遇到一些无聊的人去给我的网站上波强度，所以直播的时候用域名即可，本地随便配置一个代理就好

```bash
vim /etc/hosts

# 添加如下
[ip] xxx.com

# 示例
121.1.1.1 fenglive.com
```

## 本地端口转发 ✅

用了一会腾讯云就提示让我去备案，所以选择本地端口转发的方式，甚至可以不开防火墙策略

如果文档要补充的话， ssh -L 需要配置 3011 和 3010 端口转发，相当于做一层本地端口转发，本地（localhost）访问的是 ssh 对应的端口服务

**注意**：转发 API 连接的窗口不能关，否则就失效了

```bash
ssh -L [服务器端口]:localhost:[本地端口] [服务器用户名]@[服务器域名或者 IP 地址]

# 示例
ssh -L 3011:localhost:3011 root@fenglive.icu
ssh -L 3010:localhost:3010 root@fenglive.icu
```

## ranger ✅

[GitHub ranger](https://github.com/ranger/ranger)

安装

```bash
pip install ranger-fm
```

使用

```bash
ranger
```

初始化配置文件

```bash
ranger --copy-config=all
```

直接从本地复制 `~/.config/ranger` 到服务器即可

补充：服务器临时废纸篓地址

```bash
/root/.local/share/Trash/files
```
