---
title: 关于ArchLinux下一些软件使用
date: 2024-05-29T20:07:11+08:00
tags:
   - Arch
   - MPV
   - Aria2
   - CoreCtrl
---
### 下载工具
- ##### Aria2
   - 前端使用浏览器拓展 [Aria2 Explorer](https://aria2e.com/),后端使用 [aria2-fast/archlinuxcn](https://aur.archlinux.org/packages/aria2-fast)
  - 关于配置，有自己的配置可以将`aria2.conf`放入`~/.aria2/`中，如果没有配置可以参考[P3TERX维护的配置](https://github.com/P3TERX/aria2.conf) 注意修改成适合自己的配置。
  - 注意配置用户服务，session等，yay接管，这些均可以参考[ArchWiki](https://wiki.archlinuxcn.org/wiki/Aria2#%E6%8F%90%E7%A4%BA%E4%B8%8E%E6%8A%80%E5%B7%A7)
  - 前端链接时，可以将RPC地址协议改为 `ws://...` 避免HTTP轮询。

### 系统工具
- ##### [CoreCtrl](https://gitlab.com/corectrl/corectrl/)
  - Cpupower_GUI在我这台8845H本上有点问题，最大频率只显示3800MHz。故选择其他管理程序。(补充 是调速驱动问题 联想在笔记本bios中不给开放一些配置项导致无法更换新调速器。
  - [CoreCtrl](https://gitlab.com/corectrl/corectrl/) 是一个自由开源的GNU/Linux应用程序，允许您使用应用程序配置文件轻松控制计算机硬件。它旨在为普通用户提供灵活、舒适、方便的使用。
  - 一个较为好用的CPU与GPU调度程序，更方便的管理功耗、调度等等。
  - KDE设置开机自动启动，在参数中加入 `--minimize-systray` 开机时最小化启动。
  - 不提示输入密码、AMDGPU完整控制参考[这里](https://gitlab.com/corectrl/corectrl/-/wikis/Setup)
- ##### [Lan Mouse](https://github.com/feschber/lan-mouse):
  - 一个新局域网鼠标、键盘透传项目，支持Windows、Mac、Linux，还蛮好用的。以后会开一篇新Post细嗦。
### 媒体
- ##### MPV
  - 因为我是AMD设备，使用原版[mpv-git]()在使用着色器时出奇的卡，且无法调用wayland渲染窗口。最后选择了[mpv-amd-full-git/aur](https://aur.archlinux.org/packages/mpv-amd-full-git)
  - 若没有自己的配置，MPV配置可以参考 [MPV_lazy](https://github.com/hooke007/MPV_lazy/releases) `./portable_config`，修改完成后将配置全部放入 `~/.config/mpv/` 中，基本上只需修改 `mpv.conf` 音频相关配置删除，基础按自己窗口显示服务修改，基础配置见下方：
  - 在MPV_lazy 2024v1 版更新中，将默认右键菜单换成了原生样式，在我这里无法正常显示，需要修改 `input_uosc.conf` 右键绑定为 `MBTN_RIGHT script-binding uosc/menu`

mpv.conf:
```conf
...
 ########
 # 基础 #
 ########

 vo = gpu-next
 gpu-context = waylandvk
 gpu-api = vulkan
 hwdec = yes
 hwdec-codecs = h264,hevc,vp8,vp9,av1
...
```
- ##### LX Music
  - 因为你我都懂的原因，音源基本全🐔了，之前用惯了，目前当作一个本地播放器，如果有需要转其他项目或自建音源吧。
- 
### Windows 程序
- Protonup Qt
  - 一个好用的wine/proton多版本安装器，可以给steam、lutris等安装。
- Lutris
  - 虽说是一个游戏库，但里面自带成套的容器管理很香(至少比steam那套好用)，自带winetricks。
- [ProtonDB](https://www.protondb.com/)
   - 如果有游戏需求，且不能正常使用，可以看看这里，一般都会有大佬给出的解决方法。
 
靠这些，基本上Windows常见程序、游戏可以正常使用了，如果有问题可以参考我 [Wine](http://localhost:4000/tags/Wine/) 下的其他Post。( 挖个坑 以后填

### Android 程序


### 美化
- ##### 终端
  
- ##### 主题
  
- ##### 开始菜单
  
- ##### 任务栏


