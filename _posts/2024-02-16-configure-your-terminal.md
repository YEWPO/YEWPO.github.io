---
title: "Configure your terminal"
layout: post
date: 2024-02-16 22:44
image: /assets/images/markdown.jpg
headerImage: false
tag: 
- tmux
- shell
- nvim
star: true
category: blog
author: yewpo
description: Configure your terminal to look better!
---
> 抛弃`bash`，享受`zsh`
>
> `>`表示命令行
>
> 需要从`github`下载一些工具
>
> 更多好的插件遇到了尽量会在这个文档中补充

## Nerd Font

> Iconic font aggregator, collection, and patcher
>
> 提供了大量的图标，也提供了很多编程用的字体。
>
> 安装这些字体，以便下面这些插件的效果可以在你的终端上正常显示。
>
> 安装字体后，需要修改系统字体选项；或者，只修改终端的字体选项。

![nerd](https://www.nerdfonts.com/assets/img/sankey-glyphs-combined-diagram.png)

### 下载

官网：[nerd font](https://www.nerdfonts.com/)

选择自己喜欢的字体下载，并在系统中安装。如果你GUI桌面，可以直接打开下载的字体文件，并点击安装。如果用的非GUI桌面，参考下面示例。

如果你有选择恐惧症，可以使用下面推荐设置（但不是最好的）

```shell
> mkdir -p ~/.local/share/fonts
> cd ~/.local/share/fonts && curl -fLo "Droid Sans Mono for Powerline Nerd Font Complete.otf" https://github.com/ryanoasis/nerd-fonts/raw/master/patched-fonts/DroidSansMono/complete/Droid%20Sans%20Mono%20Nerd%20Font%20Complete.otf
> fc-cache -f -v
```

### 设置默认字体

系统设置：在你的系统设置里搜索字体选项。实在不会，试试`STFW`方法？

具体每个终端的修改方法：https://github.com/romkatv/powerlevel10k#manual-font-installation。

## Zsh

> `zsh`由`Paul Falstad`开发，但取名于`Zhong Shao`教授。

### 安装

```shell
> sudo apt update; sudo apt install zsh
```

设置`zsh`为你的默认`shell`：

```shell
> sudo chsh -s $(sudo which zsh)
```

重启电脑后可完成设置。

### zsh 框架

> Oh My Zsh is a delightful, open source, community-driven framework for managing your Zsh configuration. It comes bundled with thousands of helpful functions, helpers, plugins, themes, and a few things that make you shout...
>
> "Oh My ZSH!"

`oh my zsh`官方效果图：

![zsh](https://cloud.githubusercontent.com/assets/2618447/6316862/70f58fb6-ba03-11e4-82c9-c083bf9a6574.png)

#### 获取`Oh My ZSH`

```shell
>>> sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

重启`shell`，你会看到默认配置的`oh my zsh`。现在看看用户的主目录的`.zshrc`文件，你基本可以靠自己阅读配置注解改改他的默认配置。

**从`.bashrc`中复制你原来自己增加的配置，原来自带的配置不要复制**，尤其是`PATH`这样的配置（否则，你会发现原来`bash`可以运行的程序在`zsh`中提示不存在该命令？）。像`.zshrc`的第一个配置，你需不需要加上`~/.local/bin`呢？

#### 主题

[themes](https://github.com/ohmyzsh/ohmyzsh/wiki/Themes)，这里有完整的`zsh`自带主题介绍，选择你自己喜欢的吧。在页面的最下端还有非自带的主题的介绍，这些非自带主题就需要自己花时间折腾，但是最终效果一般会比自带的好，比如下面推荐的非自带主题。

**推荐**

主题和官网链接：[powerlevel10k](https://github.com/romkatv/powerlevel10k)

官方效果图：

![p10k](https://raw.githubusercontent.com/romkatv/powerlevel10k-media/master/prompt-styles-high-contrast.png)

安装：

```shell
>>> git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
```

之后，修改`.zshrc`中的主题选项为`p10k`。

配置方法：

再次重新运行`zsh`会有`p10k`引导教程。更细的配置（比如添加显示的内容，修改分隔符号等等）请查看官方文档，网页连接已经在超连接中给出。

#### 插件

[plugins](https://github.com/ohmyzsh/ohmyzsh/wiki/Plugins)，这里有完整的插件介绍，选择你需要的插件来提高你的工作效率。

**推荐**

- `git`：一些`git`的快捷操作。
- `zsh-syntax-highlighting`：`shell`语法高亮，这样你就不会一直敲着白色的命令辣。**需要自己搜索安装，不能在设置中直接设置**，链接：[zsh-syhntax-hightlighting](https://github.com/zsh-users/zsh-syntax-highlighting)
- `zsh-autosuggestions`：命令建议，怕忘记之前输入过的命令，试试这个吧，还可以一键补全。**需要自己搜索安装，不能在设置中直接设置**，链接：[zsh-autosuggestions](https://github.com/zsh-users/zsh-autosuggestions)
- `colored-man-pages`：每次看`man`的时候只有单调的文本？这个让你`man`阅读的更加舒服。
- `tmux`：一些`tmux`的快捷操作。
- `web-search`：有了他，你就可以在终端百度或者必应或者谷歌辣。
- `autojump`：结合`autojump`，让您更加方便地在文件夹之间进行跳转。

## Tmux

> 宁愿开多个终端/ssh连接, 也不愿意花时间找找有没有tmux ，
>
> 于是用鼠标来回切换, 浪费不必要的时间。 ——出自ysyx

从引语就知道为什么要用`tmux`了吧。

`tmux wiki`：https://github.com/tmux/tmux/wiki

### 安装

```shell
>>> sudo apt install tmux
```

### 配置

在你的主目录下创建`.tmux.conf`，初步的配置：

```\
set -g prefix C-a # 设置前缀键，默认的C-b有点不人性化 

# 新建窗口用父亲的工作目录
bind-key c new-window -c "#{pane_current_path}"
bind-key % split-window -h -c "#{pane_current_path}"
bind-key '"' split-window -c "#{pane_current_path}"

# 导航方式如同vi，默认是emac
set-window-option -g mode-keys vi
```

### 插件

> 默认的下面的状`tmux`太丑？试试`.tmux`或者是`powerline`。

#### .tmux

> 有`oh my zsh`，当然就有`oh my tmux`（毫无逻辑关系）。`.tmux`就是这样的`oh my tmux`。
>
> 同时他也是可以`tmux`的配置包。

仓库地址：https://github.com/gpakosz/.tmux

官方效果图：

![tmux](https://cloud.githubusercontent.com/assets/553208/19740585/85596a5a-9bbf-11e6-8aa1-7c8d9829c008.gif)

##### 安装

```shell
> cd
> git clone https://github.com/gpakosz/.tmux.git
> ln -s -f .tmux/.tmux.conf
> cp .tmux/.tmux.conf.local .
```

**不要忘记命令中的点**

##### 配置

`.tmux.conf.local`文件已经有详细的注释，可以按照注释修改配置文件。

比如，修改状态块分隔符，文件中搜索`seperator`。

#### powerline

> 全面的状态栏工具，不仅仅只向`tmux`提供，同时也向`bash, zsh, nvim`等提供状态栏。

##### 安装

安装方法见[官方文档](https://powerline.readthedocs.io/en/master/installation.html)

##### tmux状态栏

安装方法见[官方文档](https://powerline.readthedocs.io/en/master/usage/other.html#tmux-statusline)

##### 配置

这个就需要自己阅读[配置文档](https://powerline.readthedocs.io/en/master/configuration.html)，然后修改或着自己编写相应的代码了。

## Vim

> 还在使用普通编辑器，还在用鼠标或者键盘上下进行代码片段跳跃？来用用`vi`吧。
>
> 什么？你还在用`vi`，来用用`vi`改进版`vim`吧。
>
> 不会还有人用`vim`吧，来试试全新内核`nvim(neovim)`[neovim](https://github.com/neovim/neovim)。
>
> `nvim`配置太麻烦了，来用用基本免配置的`lvim`吧。
>
> **vim的插件都来自github上的开源软件，建议以适当的方式访问**

### Nvim

#### 安装

对于`Ubuntu`用户，不要在`apt`中安装，版本太老，建议在`Github`上下载安装包。

发行版下载源和安装说明：https://github.com/neovim/neovim/releases/tag/stable

#### 配置

这个我还真没法教，每个人都有独特的代码习惯和审美特点。[这里](https://github.com/rockerBOO/awesome-neovim)有全部的插件介绍，选择自己喜欢的进行配置吧。

[neovimcraft](https://neovimcraft.com/)集聚了优秀的插件和最新的插件，还有插件排行榜。

但是我还是有我自己的配置文件，并在`Github`建有仓库，名叫`Ynvim`。基本满足了我自己需求；安装方法和配置参见[nvim Config](http://43.139.35.156/75/nvim-config/)。

自己配置的效果图：

![image-20230207113218071](https://raw.githubusercontent.com/YEWPO/yewpoblogonlinePic/main/image-20230207113218071.png)

**但是都是一些简单的配置，具体配置方法，请在上文中的插件链接中找到对应的插件文档，阅读文档进行配置**。

### Lvim

不想自己配置，想直接使用现代化编辑器，`lvim`确实是一个不错的选择。

官网：[lunarvim](lunarvim.org)

官方效果图：

![lvim](https://user-images.githubusercontent.com/29136904/191624942-3d75ef87-35cf-434d-850e-3e7cd5ce2ad0.png)

#### 安装

- Make sure you have installed the latest version of [`Neovim v0.8.0+`](https://github.com/neovim/neovim/releases/latest).
- Have [`git`](https://cli.github.com/), [`make`](https://www.gnu.org/software/make/), [`pip`](https://pypi.org/project/pip/), [`python`](https://www.python.org/) [`npm`](https://npmjs.com/), [`node`](https://nodejs.org/) and [`cargo`](https://www.rust-lang.org/tools/install) installed on your system.
- [Resolve `EACCES` permissions when installing packages globally](https://docs.npmjs.com/resolving-eacces-permissions-errors-when-installing-packages-globally) to avoid error when installing packages with npm.
- [`PowerShell 7+`](https://learn.microsoft.com/en-us/powershell/scripting/whats-new/migrating-from-windows-powershell-51-to-powershell-7?view=powershell-7.2) (for Windows)

```shell
> LV_BRANCH='release-1.2/neovim-0.8' bash <(curl -s https://raw.githubusercontent.com/lunarvim/lunarvim/fc6873809934917b470bff1b072171879899a36b/utils/installer/install.sh)
```

安装完成后，运行`lvim`，开箱即用。

### NvChad

> 目前排行榜第一，但是该项目只提供了基本的`nvim`配置，更多的选项需要自己配置，所以，该项目需要有一定配置经验和水平的人使用。初学者使用该项目较为困难。
>
> 建议能用`lvim`就用`lvim`。`lvim`的名气正在快速增长中。

官网：https://nvchad.com/

官方效果图：

![NvChad banner screenshot](https://nvchad.com/banner.webp)

#### 安装

- You should be an existing Vim user or keen to learn Neovim and NvChad (through these docs).
- [Neovim 0.8.0](https://github.com/neovim/neovim/releases/tag/v0.8.0), if your distro/OS doesn't have it then try [neovim version manager](https://github.com/MordechaiHadad/bob).
- [Use a Nerd Font](https://www.nerdfonts.com/) in your terminal emulator.
- Make sure to delete this folder `~/.local/share/nvim` on Linux/macOS or `~\AppData\Local\nvim` and `~\AppData\Local\nvim-data` on Windows.

```shell
> git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1 && nvim
```

### 使用他们

上述介绍的两个版本，以及我自己提供的配置，为了更好的使用他们（比如快捷方式），需要你去读读他们的**文档**。不然，就不如使用你原来的IDE啦。

如果你想学习如何使用`vim`，可以试试下面这个命令：

```shell
>>> nvim +Tutor
```

## 杂项

### `Linux`扩展工具

#### ripgrep

> grep的替代品，使用和速度上都要好于grep。

安装：

```shell
> sudo apt install ripgrep
```

#### autojump

> 一种更快的方式进行目录跳转。

对于`oh-my-zsh`的安装方法：在`.zshrc`的插件中，添加`autojump`。

其他平台的安装方法：https://github.com/wting/autojump#installation

#### fdfind

> find的替代品，更加的好用和快捷。

安装源：https://github.com/sharkdp/fd#installation

```shell
> sudo apt install fd
```

### lazygit

> 宁愿把项目简单复制好几份, 也不愿意用git来做版本控制，
>
> 于是版本管理越来越混乱, 将来不得不投入更多时间。 ——出自ysyx

但是，`git`接口是在太难用了；好在有`tmux`的`git`插件，但是还有更好用的。

链接：[lazygit](https://github.com/jesseduffield/lazygit)

效果预览：

![lg](https://github.com/jesseduffield/lazygit/raw/assets/staging.gif)

安装根据系统安装方法不同，请自己阅读[官网文档](https://github.com/jesseduffield/lazygit#installation)。

### pwndbg

> 原始的gdb的调试也不够人性化，试试这个

链接：[pwndbg](https://github.com/pwndbg/pwndbg)

效果图：

![image-20230206213710490](https://raw.githubusercontent.com/YEWPO/yewpoblogonlinePic/main/image-20230206213710490.png)

安装方法：

```shell
> git clone https://github.com/pwndbg/pwndbg
> cd pwndbg
> ./setup.sh
```

### mobile ssh

> ssh 是一个强大工具，但是存在一个小小的问题，网络一不小心断了，连接也就断了。

`mosh`的想法就是解决这个问题，它采用`UDP`建立连接，即使断了，也会尝试连接。

链接：[mosh官网](https://mosh.org/)

安装方法：

```shell
> sudo apt install mosh
```

### nvm

> 用于管理`node`和`npm`版本，可以使用`root`权限。

链接：[nvm](https://github.com/nvm-sh/nvm)

安装方法：

```shell
>>> curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.3/install.sh | bash
```

## More

> 更多好用的工具需要你我的探索

### 终端模拟器

#### Windows

对于`Windows`用户，我推荐`Tabby`，比较现代化。同样它提供了`Linux`和`Mac`版本。

链接：[tabby](https://github.com/Eugeny/tabby)

![img](https://github.com/Eugeny/tabby/raw/master/docs/readme.png)

#### Linux

网上的推荐是`kitty`，采用了`GPU`加速，提供了更多的设置选项，包括主题。

优点：提供了类似tmux的多路复用操作，便捷键要比tmux友好，但是UI不如自己配置的tmux。

效果图：

![image-20230206214056682](https://raw.githubusercontent.com/YEWPO/yewpoblogonlinePic/main/image-20230206214056682.png)

链接：[kitty](https://github.com/kovidgoyal/kitty)

## 学习使用工具

> 即使给你推荐再多的工具，你不知道怎么用，这不有点浪费电脑空间

学习方法：

- `help`，`man`命令行工具可能有其他工具的介绍
- 官方的手册或者是视频教程
- 动手实践，不实际使用你就忘了
- 遇到问题，尝试用`google`搜索一下
- 你觉得使用比较麻烦的时候，多半有快捷操作，建议搜索一下

