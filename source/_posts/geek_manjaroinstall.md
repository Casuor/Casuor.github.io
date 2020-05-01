---
title: Manjaro install
categories: Geek
photos: http://yanxuan.nosdn.127.net/f6281a7e289846fd355495634c9510d5.png
date: 2020-01-10
---
## manjaro config


     sudo pacman-mirrors -i -c China -m rank
     sudo pacman -Syy

     sudo pacman -S nano
    nano /etc/pacman.conf



    [archlinuxcn]
    SigLevel = Optional TrustedOnly
    Server = https://mirrors.ustc.edu.cn/archlinuxcn/$arch

    sudo pacman -S archlinuxcn-keyring
    sudo pacman -Syyu



    sudo pacman -S fcitx-im #全部安装
    sudo pacman -S fcitx-configtool
    sudo pacman -S fcitx-sogoupinyin


    nano ~/.xprofile



    export GTK_IM_MODULE=fcitx
    export QT_IM_MODULE=fcitx
    export XMODIFIERS="@im=fcitx"
    #restart


    sudo pacman -S  yay
    yay -S octopi


## [application list]

[latte-dock layout](https://store.kde.org/browse/cat/417/order/latest/)
    
    latte-dock
    typora
    chrome
    visual studio code
    jetbrains-toolbox
    wps-office
    
    sudo pacman -S wps-office-mui-zh-cn
    sudo pacman -S ttf-wps-fonts
    
    electron-netease-cloud-music
    bleachbit 
    baidunetdisk
    spotify
    zsh
    
    sudo nano /etc/hosts
    199.232.28.133 raw.githubusercontent.com
    
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    
    sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
    
    
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    
    git clone git://github.com/zsh-users/zsh-autosuggestions $ZSH_CUSTOM/plugins/zsh-autosuggestions
    
    git clone https://github.com/paulirish/git-open.git $ZSH_CUSTOM/plugins/git-open
    
    git clone https://github.com/lukechilds/zsh-nvm ~/.oh-my-zsh/custom/plugins/zsh-nvm
    #Zsh plugin for installing, updating and loading nvm
    #地址：https://github.com/lukechilds/zsh-nvm
    
    sudo pacman -S autojump
    #plugins=(git zsh-syntax-highlighting zsh-autosuggestions git-open vscode sublime z zsh-nvm autojump)
    
    #source ~/.zshrc
    
    
    nvm install 12.16.2
    npm install nrm -g
    nrm use taobao
    
    [ssr配置](https://www.jianshu.com/p/1a1bbff13e22)
    
    wget http://www.djangoz.com/ssr#//github.com/the0demiurge/CharlesScripts/blob/master/charles/bin/ssr
    
     sudo mv ssr /usr/local/bin
     sudo chmod 766 /usr/local/bin/ssr
     ssr install
     ssr config
    
    
    #设置开机启动
    #在/usr/lib/systemd/system/中加入ssr.service
    [Unit]
    Description=AutoRunSSR
    
    [Service]
    Type=forking
    ExecStart=ssr start 
    
    [Install]
    WantedBy=multi-user.target
    
    
    systemctl enable ssr.service
    systemctl start ssr.service
    #查看状态
    systemctl status ssr.service
    

![](http://yanxuan.nosdn.127.net/f6281a7e289846fd355495634c9510d5.png)
