# CasaOS_OneCloud

CasaOS_玩客云搞基计划。

本项目收集一些玩客云可以使用的 Docker 镜像以及解决一些问题。

> 始于玩客云(arm/v7)，不止于玩客云


### 第三方应用

[AppFile](/AppFile) 文件夹收集一些好用的镜像 JSON 文件，尽可能方便地扩展CasaOS的功能。

使用方法：应用中心-自定义安装-右上角导入-AppFile

部分镜像你可能需要创建文件夹或者修改一些信息，请根据实际情况修改。

### 使用笔记

使用笔记&技巧 [README_skill.md](/README_skill.md) 文件记录本人使用玩客云 Armbian+CasaOS 遇到的一些坑和使用技巧。

仅 Armbian 中测试，不一定适用其他系统和架构，请自行甄别。

## CasaOS

### 介绍

CasaOS项目官方 https://github.com/IceWhaleTech/CasaOS

《CasaOS—— 一个简单，易于使用，优雅的开源家庭云系统》
https://mp.weixin.qq.com/s/1oMywRTbmUADLOlSefvd9A

https://www.bilibili.com/video/BV1X94y1Z7sA

### 安装

以下脚本基于[官方脚本](https://get.casaos.io) v0.3.7，仅修改了198~202行 GitHub 加速，423行 Docker 安装加速。

```sh
wget -qO- https://gcore.jsdelivr.net/gh/Cp0204/Casaos_Onecloud@main/script/casaos.sh | bash
```

or

```sh
curl -fsSL https://gcore.jsdelivr.net/gh/Cp0204/Casaos_Onecloud@main/script/casaos.sh | bash
```

### 卸载

```sh
casaos-uninstall
```

## 其他

### Docker介绍

Docker 是一个开源的应用容器引擎，可以让开发者打包他们的应用以及依赖包到一个轻量级、可移植的容器中，然后发布到任何流行的 Linux 机器上，也可以实现虚拟化。

容器是完全使用沙箱机制，相互之间不会有任何接口（类似 iPhone 的 app）,更重要的是容器性能开销极低。

如果你希望了解Docker，请点击这里  

https://www.runoob.com/docker/docker-tutorial.html

### SMB共享

CasaOS 目前暂不支持 samba 共享的权限控制，如果需要权限控制，需关闭CasaOS内置共享，并用第三方镜像：

https://github.com/dperson/samba


