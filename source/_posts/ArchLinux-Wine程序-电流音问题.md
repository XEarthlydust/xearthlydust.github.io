---
title: ArchLinux 下 Wine兼容层程序 电流音问题解决方案
date: 2024-05-29 10:12:33
tags: 
   - Arch
   - Wine
   - PipeWire
   - PulseAudio
---
### 前言

24年4月入手了一台Thinkbook14+(2024)，由于饱受Windows的折磨(神笔微软电脑管家，OfficePlus)，故到手时安装使用ArchLinux。
此为小问题的解决记录，存档备忘，若有帮助，倍感荣幸。

### 问题

本人使用PipeWire作为音频后端，主机音频与wine程序同时运行时，喇叭时常有刺耳的电流音。

根据搜索，在PulseAudio后端下，Wine有已知的音频断断续续BUG(可能表现也为电流音)，这点在 [WineWiki](https://wiki.winehq.org/Sound) 和 [WineBug](https://bugs.winehq.org/show_bug.cgi?id=39814) 都有提到。

### 分析与解决

- ##### PulseAudio:
关于 PulseAudio 解决方案，有人提到是缓存问题，解决方案参考 [Debian-PulseAudio](https://wiki.debian.org/PulseAudio#Various_problems_with_Skype_and_Wine) (没有使用PulseAudio的设备，仅供参考

- ##### PipeWire:
开关 EasyEffects，仍有电流音。
查看 Winecfg 当前调用驱动是调用 PulseAudio 后端。故猜想同样是缓存值太低导致音频异常。
![](/image/ArchLinux-Wine程序-电流音问题/winecfg01.png)

尝试修改PipeWire缓存：
首先用 pw-top 命令查看 quantum ，然后用这个命令增加 quantum 值，直到音频变得更加平滑。

```bash
pw-metadata -n settings 0 clock.force-quantum 2048
```

一旦你找到适合你情况的 quantum 值(对我的设备 `quantum = 2048` 在以往场景下未出现异常，故采用此值)。
可以通过创建一个内容如下的配置文件 `
~/.config/pipewire/pipewire.conf.d/choppy-under-load.conf`，并重启与 pipewire 相关的守护程序，使这个值永久化。

```bash
context.properties = {
   default.clock.force-quantum = 2048
   default.clock.quantum = 2048
   default.clock.min-quantum = 2048
}
```

### 参考链接
- [WineWiki](https://wiki.winehq.org/Sound)
- [WineBug](https://bugs.winehq.org/show_bug.cgi?id=39814)
- [Debian-PulseAudio](https://wiki.debian.org/PulseAudio#Various_problems_with_Skype_and_Wine)
- [Debian-PipeWire](https://wiki.debian.org/zh_CN/PipeWire#A.2BVyia2I0fj318.2B37fTgqX85iRTg16M1ua-)