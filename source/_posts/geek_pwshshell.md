---

title: 必知必会的Powershell指令
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/socks.png
date: 2020-05-22

---

# 必知必会的Powershell指令
### Get-Command
>gcm  
>
>获取全部命令
### Get-Help  
>Get-Help 指令名
>
>查看某一命令的具体使用方法
### Clear-Host
>clear/cls
>
>清屏
### Get-Location
>gl/pwd
>
>输出当前所在目录
### Set-Location
>sl/cd 
>
>cd ~ #返回根目录
>
>cd.. #返回上级目录
>
>设置当前所在目录
### Get-ChildItem
>dir/ls
>
>输出当前目录子项
### Get-Item
>gi 文件/目录名
>
>获取子项信息
>
>gi x*
>
>使用*通配符筛选文件,相当于linux find指令
### New-Item
>ni 文件名
>
>创建文件
>
>mkdir   md
>创建目录
### Move-Item
>mv 文件名 目录名
>
>移动文件
>
>mv 目录名 目录名
>
>移动目录

### Copy-Item
>cp 文件名 目录名
>
>将文件复制到某目录
### Rename-Item
>ren 原文件名 新文件名
>
>重命名文件或目录
### Remove-Item
>rm 文件名/or目录/文件名
>
>删除文件或目录
>

### Add-Content
>ac 文件名
>
>文件追加内容
### Set-Content
>sc 文件名
>
>设置文件内容，会覆盖原内容
### Clear-Content
>clc 文件名
>
>清楚文件内容
### Get-Service
>gsv
>
>获取当前运行的服务
### Get-Process
>gps
>
>获取当前运行的进程
### Stop-Process
>kill/spss 进程名
>
>关掉相应的进程
### Start-Process 
>start 进程名/或其他参数
>
>start . 资源管理器打开当前所在目录
>
>开启某个进程
### Get-Alias
>alias 
>
>输出当前存在的别名
>
>设置别名Set-Alias(sal)


