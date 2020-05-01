---
title: Oh-my-zsh for Manjaro
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/xiangxiang.jpg
date: 2020-01-13
---
# oh my zsh
## install
#### install zsh

    #查看是否已安装
    zsh --version
    ＃查看已安装的shell
    cat /etc/shells 


    #安装zsh
    yay -S zsh
    #pacman -S zsh



    #切换为zsh
    #chsh -s /bin/zsh
    chsh -s $(which zsh)



    #查看当前shell
    #$SHELL --version
    echo $SHELL



#### install oh-my-zsh

    sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"


    sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"

## theme
###  directory

    cd ~/.oh-my-zsh/themes
    ls

### change

    nano ~/.zshrc
    #ZSH_THEME="agnoster"
    #为agnoster添加时间显示
    echo "RPROMPT='[%*]'" >> $ZSH/themes/agnoster.zsh-theme
    source ~/.zshrc


### edit zsh-theme
#### agnoster.zsh-theme conf

    code agnoster.zsh-theme


>[Powerline-patched font]
In order for this theme to render correctly, you will need a [Powerline-patched font]

PS:已经有了，不用安装

>[Solarized theme]
默认为dark,可切换light

>[Show informations]
Like most prompts, it will only show git information when in a git working directory.
However, it goes a step further: everything from the current user and
hostname to whether the last call exited with an error to whether background
jobs are running in this shell will all be displayed automatically when
appropriate.

PS:并非所有theme显示时间

#### edit

    # Context: user@hostname (who am I and where am I)
    #user@hostname <=> %n@%m
    #太长删其一即可
    prompt_context() {
      if [[ "$USER" != "$DEFAULT_USER" || -n "$SSH_CLIENT" ]]; then
        prompt_segment black default "%(!.%{%F{yellow}%}.)%n@%m"
      fi
    }


![](https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/20200113/zshcontext.gif)

## plugins

### ｄefault

    ＃tlsr
    cd ~/.oh-my-zsh/plugins
    ls

#### 启用插件

    nano ~/.zshrc
    #plugins=(git zsh-syntax-highlighting zsh-autosuggestions git-open vscode npm npx sublime z)

PS:空格问题

### custome 
>Also follow these steps if you want to override plugins that ship with your oh-my-zsh installation. To override a plugin with a custom version, put your custom version at $ZSH_CUSTOM/plugins/<plugin_name>/. For example, if it's the rvm plugin you want to override, create the directory custom/plugins/rvm and place a file called rvm.plugin.zsh inside of it.

PS:dont　remember add `<plugin_name>` to `.zshrc`

#### example
1.Clone this repository in oh-my-zsh's plugins directory:

    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting

PS:自定义plugins-location
git clone url `${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/`plugins-name,额不早为啥这样写，应该是和`~/.zshrc`文件相关

2.Activate the plugin in ~/.zshrc:

    plugins=( [plugins...] zsh-syntax-highlighting)

3.Restart zsh (such as by opening a new instance of your terminal emulator).

### last preview
![](https://cdn.jsdelivr.net/gh/Casuor/CDN/Posts/Image/20200113/ohmyzsh.png)