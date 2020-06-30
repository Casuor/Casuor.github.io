
---

title: scoop
categories: Geek
photos: https://cdn.jsdelivr.net/gh/Casuor/CDN@latest/Posts/Image/Common/kawayi0.jpg
date: 2020-04-06

---

[reference](https://alertcode.top/windows%E4%B8%8B%E5%8C%85%E7%AE%A1%E7%90%86%E5%B7%A5%E5%85%B7scoop%E7%9A%84%E4%BD%BF%E7%94%A8/)

```
#修改hosts
#github
140.82.114.3 github.com
185.199.110.153  assets-cdn.github.com
199.232.69.194 github.global.ssl.fastly.net
199.232.68.133 raw.githubusercontent.com

Set-ExecutionPolicy RemoteSigned -scope CurrentUser
$env:SCOOP='D:\Scoop'
[Environment]::SetEnvironmentVariable('SCOOP', $env:SCOOP, 'User')
$env:SCOOP_GLOBAL='D:\GlobalScoopApps'
[Environment]::SetEnvironmentVariable('SCOOP_GLOBAL', $env:SCOOP_GLOBAL, 'Machine') #此步骤管理员运行
#确保raw.githubusercontent.com可以访问
Invoke-Expression (New-Object 
System.Net.WebClient).DownloadString('https://get.scoop.sh')
```

```
scoop install sudo -g
#ssr代理
scoop config proxy 127.0.0.1:1080
#scoop config rm proxy
scoop install aria2 #喵的死活下不动
scoop install git
scoop update
Set-ItemProperty 'HKLM:\SYSTEM\CurrentControlSet\Control\FileSystem' -Name 'LongPathsEnabled' -Value 1
scoop install innounp
scoop install dark
scoop checkup
scoop bucket add extras
scoop install typora
scoop install vscode
code  $env:LocalAppData\Packages\Microsoft.WindowsTerminal_8wekyb3d8bbwe\LocalState\settings.json

```

```powershell
scoop install figlet
scoop install cowsay
scoop bucket add dorado https://github.com/h404bi/dorado
sudo scoop install trash -g
sudo scoop install nvm -g
scoop bucket add Ash258 'https://github.com/Ash258/Scoop-Ash258.git'
scoop install carnac
scoop bucket add iszy 'https://github.com/ZvonimirSun/scoop-iszy.git'
scoop install wechat
scoop install qq-dreamcast
scoop install utools
scoop install switchhosts
scoop install scoop bucket add my-scoop-bucket https://github.com/destinyenvoy/my-scoop-bucket
scoop install gvim
#设置别名
scoop alias add i 'scoop install $args[0]'
scoop alias add rm 'scoop uninstall $args[0]'
scoop alias add ls 'scoop list' 'List installed apps'
scoop alias add up 'scoop update $args[0]' 'Update apps, or Scoop itself'
```

> 7zip 19.00
  anaconda3 2020.02 [dorado]
  aria2 1.35.0-1
  carnac 2.3.13 [extras]
  clash-for-windows  *failed*
  ColorTool 1904.29002
  cowsay 0.2013.07.19
  dark 3.11.2
  dismplusplus 10.1.1001.10 [extras]
  everything 1.4.1.969 [extras]
  fiddler 5.0.20202.18177 [extras]
  figlet 1.0-go
  firefox current [extras]
  git 2.26.2.windows.1
  github 2.5.2 [extras]
  googlechrome 81.0.4044.138 [extras]
  gow 0.8.0
  innounp 0.49
  jetbrains-toolbox 1.17.7018 [extras]
  kate 20.04.1-893 [extras]
  mubu 1.2.4 [dorado]
  mysql 8.0.20
  netease-music 2.7.1.198242 [iszy]
  nircmd 2.86 *global*
  notion 2.0.8 [Ash258]
  nvm 1.1.7 *global*
  oraclejdk8 8u231 [iszy]
  powertoys 0.18.2 [extras]
  pwsh-preview 7.1.0-preview.3 [Ash258]
  python 3.8.3
  QtScrcpy 1.3.5 [dorado]
  rufus 3.10 [extras]
  screentogif 2.24.2 [extras]
  sudo 0.2020.01.26 *global*
  switchhosts 3.5.4 [extras]
  trash 2.0.0 *global* [dorado]
  typora 0.9.89 [extras]
  vscode 1.46.1 [extras]
  wechat nightly-20200515 [dorado]


