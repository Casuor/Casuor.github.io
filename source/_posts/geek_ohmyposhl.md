---
title: Oh-my-posh for Windows
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/xiangxiang.jpg
date: 2020-01-24
---

# oh my posh for windows

## main

### install&config for powershell

    Install-Module posh-git -Scope CurrentUser
    Install-Module oh-my-posh -Scope CurrentUser
    $profile
    cd C:\Users\16877\Documents\WindowsPowerShell\
    ls
    New-Item "Microsoft.PowerShell_profile.ps1" -type file
    code Microsoft.PowerShell_profile.ps1
    Import-Module posh-git
    Import-Module oh-my-posh
    Set-Theme Paradox


#### detail for teminal

    {
    "$schema": "https://aka.ms/terminal-profiles-schema", 
    "globals" : 
    {
        "alwaysShowTabs" : true,
        "copyOnSelect" : false,
        "defaultProfile": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}", 
        "initialCols" : 90,
        "initialRows" : 30,
        "requestedTheme" : "system",
        "showTabsInTitlebar" : true,
        "showTerminalTitleInTitlebar" : true,
        "wordDelimiters" : " ./\\()\"'-:,.;<>~!@#$%^&*|+=[]{}~?\u2502"
    },
    "profiles": [
        {
            "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}", 
            "name": "Windows PowerShell", 
            "commandline": "powershell.exe", 
            "hidden": false, 
            "acrylicOpacity": 0.9, 
            "colorScheme": "MaterialDark", 
            "cursorColor": "#ffea2e", 
            "cursorShape": "filledBox",  
            "fontFace": "Hack", 
            "fontSize": 12, 
            "historySize": 9001, 
            "padding": "0, 0, 0, 0", 
            "snapOnInput": true, 
            "startingDirectory": "%USERPROFILE%", 
            "useAcrylic": true
        }, 
        {
            "guid": "{0caa0dad-35be-5f56-a8ff-afceeeaa6101}", 
            "name": "cmd", 
            "commandline": "cmd.exe", 
            "hidden": false
        }, 
        {
            "guid": "{b453ae62-4e3d-5e58-b989-0a998ec441b8}", 
            "hidden": false, 
            "name": "Azure Cloud Shell", 
            "source": "Windows.Terminal.Azure"
        }
    ], 
    "schemes": [
        {
            "name": "Solarized Dark - Patched", 
            "black": "#002831", 
            "red": "#d11c24", 
            "green": "#738a05", 
            "yellow": "#a57706", 
            "blue": "#2176c7", 
            "purple": "#c61c6f", 
            "cyan": "#259286", 
            "white": "#eae3cb", 
            "brightBlack": "#475b62", 
            "brightRed": "#bd3613", 
            "brightGreen": "#475b62", 
            "brightYellow": "#536870", 
            "brightBlue": "#708284", 
            "brightPurple": "#5956ba", 
            "brightCyan": "#819090", 
            "brightWhite": "#fcf4dc", 
            "background": "#001e27", 
            "foreground": "#708284"
        }, 
        {
            "background": "#282C34", 
            "black": "#282C34", 
            "blue": "#61AFEF", 
            "brightBlack": "#5A6374", 
            "brightBlue": "#61AFEF", 
            "brightCyan": "#56B6C2", 
            "brightGreen": "#98C379", 
            "brightPurple": "#C678DD", 
            "brightRed": "#E06C75", 
            "brightWhite": "#DCDFE4", 
            "brightYellow": "#E5C07B", 
            "cyan": "#56B6C2", 
            "foreground": "#DCDFE4", 
            "green": "#98C379", 
            "name": "One Half Dark", 
            "purple": "#C678DD", 
            "red": "#E06C75", 
            "white": "#DCDFE4", 
            "yellow": "#E5C07B"
        }, 
        {
            "name": "Material", 
            "black": "#002831", 
            "red": "#b7141f", 
            "green": "#457b24", 
            "yellow": "#f6981e", 
            "blue": "#134eb2", 
            "purple": "#560088", 
            "cyan": "#0e717c", 
            "white": "#efefef", 
            "brightBlack": "#424242", 
            "brightRed": "#e83b3f", 
            "brightGreen": "#7aba3a", 
            "brightYellow": "#ffea2e", 
            "brightBlue": "#54a4f3", 
            "brightPurple": "#aa4dbc", 
            "brightCyan": "#26bbd1", 
            "brightWhite": "#d9d9d9", 
            "background": "#eaeaea", 
            "foreground": "#232322"
        }, 
        {
            "name": "MaterialDark", 
            "black": "#212121", 
            "red": "#b7141f", 
            "green": "#457b24", 
            "yellow": "#f6981e", 
            "blue": "#134eb2", 
            "purple": "#560088", 
            "cyan": "#0e717c", 
            "white": "#efefef", 
            "brightBlack": "#424242", 
            "brightRed": "#e83b3f", 
            "brightGreen": "#7aba3a", 
            "brightYellow": "#ffea2e", 
            "brightBlue": "#54a4f3", 
            "brightPurple": "#aa4dbc", 
            "brightCyan": "#26bbd1", 
            "brightWhite": "#d9d9d9", 
            "background": "#001e27", 
            "foreground": "#e5e5e5"
        }
    ], 
    "keybindings": [
        {
            "command": "closePane", 
            "keys": [
                "ctrl+w"
            ]
        }, 
        {
            "command": "copy", 
            "keys": [
                "ctrl+c"
            ]
        }, 
        {
            "command": "duplicateTab", 
            "keys": [
                "ctrl+shift+d"
            ]
        }, 
        {
            "command": "newTab", 
            "keys": [
                "ctrl+N"
            ]
        }, 
        {
            "command": "newTabProfile0", 
            "keys": [
                "ctrl+shift+1"
            ]
        }, 
        {
            "command": "newTabProfile1", 
            "keys": [
                "ctrl+shift+2"
            ]
        }, 
        {
            "command": "newTabProfile2", 
            "keys": [
                "ctrl+shift+3"
            ]
        }, 
        {
            "command": "newTabProfile3", 
            "keys": [
                "ctrl+shift+4"
            ]
        }, 
        {
            "command": "newTabProfile4", 
            "keys": [
                "ctrl+shift+5"
            ]
        }, 
        {
            "command": "newTabProfile5", 
            "keys": [
                "ctrl+shift+6"
            ]
        }, 
        {
            "command": "newTabProfile6", 
            "keys": [
                "ctrl+shift+7"
            ]
        }, 
        {
            "command": "newTabProfile7", 
            "keys": [
                "ctrl+shift+8"
            ]
        }, 
        {
            "command": "newTabProfile8", 
            "keys": [
                "ctrl+shift+9"
            ]
        }, 
        {
            "command": "nextTab", 
            "keys": [
                "ctrl+tab"
            ]
        }, 
        {
            "command": "openNewTabDropdown", 
            "keys": [
                "ctrl+shift+space"
            ]
        }, 
        {
            "command": "openSettings", 
            "keys": [
                "ctrl+,"
            ]
        }, 
        {
            "command": "paste", 
            "keys": [
                "ctrl+shift+v"
            ]
        }, 
        {
            "command": "prevTab", 
            "keys": [
                "ctrl+shift+tab"
            ]
        }, 
        {
            "command": "scrollDown", 
            "keys": [
                "ctrl+shift+down"
            ]
        }, 
        {
            "command": "scrollDownPage", 
            "keys": [
                "ctrl+shift+pgdn"
            ]
        }, 
        {
            "command": "scrollUp", 
            "keys": [
                "ctrl+shift+up"
            ]
        }, 
        {
            "command": "scrollUpPage", 
            "keys": [
                "ctrl+shift+pgup"
            ]
        }, 
        {
            "command": "switchToTab0", 
            "keys": [
                "ctrl+alt+1"
            ]
        }, 
        {
            "command": "switchToTab1", 
            "keys": [
                "ctrl+alt+2"
            ]
        }, 
        {
            "command": "switchToTab2", 
            "keys": [
                "ctrl+alt+3"
            ]
        }, 
        {
            "command": "switchToTab3", 
            "keys": [
                "ctrl+alt+4"
            ]
        }, 
        {
            "command": "switchToTab4", 
            "keys": [
                "ctrl+alt+5"
            ]
        }, 
        {
            "command": "switchToTab5", 
            "keys": [
                "ctrl+alt+6"
            ]
        }, 
        {
            "command": "switchToTab6", 
            "keys": [
                "ctrl+alt+7"
            ]
        }, 
        {
            "command": "switchToTab7", 
            "keys": [
                "ctrl+alt+8"
            ]
        }, 
        {
            "command": "switchToTab8", 
            "keys": [
                "ctrl+alt+9"
            ]
        }
    ]
    }

## Extra

### font 

[Hack](https://github.com/source-foundry/Hack)
[Cascadia Code](https://github.com/microsoft/cascadia-code)

### colortool

    scoop install colortool
    # 注：-s 代表 schemes
    colortool -s
    # 临时查看
    colortool <主题名称>
    # 定义默认值
    colortool -d <主题名称>


## preview

![image](https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/20200124/wt.png)

## Reference

[Oh my posh](https://github.com/JanDeDobbeleer/oh-my-posh)