# README_skill

本文件记录本人使用玩客云 Armbian+CasaOS 遇到的一些坑和使用技巧。

仅 Armbian 中测试，不一定适用其他系统和架构，请自行甄别。

## 使用技巧

### 一键换源
系统源
```sh
bash <(curl -sSL https://gitee.com/SuperManito/LinuxMirrors/raw/main/ChangeMirrors.sh)
```
Docker源
```sh
bash <(curl -sSL https://gitee.com/SuperManito/LinuxMirrors/raw/main/DockerInstallation.sh)
```
### 登录SSH输出系统信息

`/etc/update-motd.d/` 以下文件设为744权限

- 10-armbian-header
- 30-armbian-sysinfo

### 修改 mac 地址
`/etc/NetworkManager/system-connections/Wired connection 1.nmconnection`
修改 cloned-mac-address=00:00:00:00:00:00

### U盘SD卡自动挂载卸载

新建 `/etc/udev/rules.d/11-auto-mount.rules` 内容如下

```
KERNEL!="sd*|mmcblk0*", GOTO="media_by_label_auto_mount_end"
SUBSYSTEM!="block",GOTO="media_by_label_auto_mount_end"
IMPORT{program}="/sbin/blkid -o udev -p %N"
ENV{ID_FS_TYPE}=="", GOTO="media_by_label_auto_mount_end"
ENV{ID_FS_LABEL}!="", ENV{dir_name}="%E{ID_FS_LABEL}"
ENV{ID_FS_LABEL}=="", ENV{dir_name}="%E{ID_FS_UUID}"
ACTION=="add", ENV{mount_options}="relatime,sync"
ACTION=="add", RUN+="/bin/mkdir -p /media/%E{dir_name}", RUN+="/usr/bin/systemd-mount -o %E{mount_options} --no-block --automount=yes --collect /dev/%k /media/%E{dir_name}"
ACTION=="remove", ENV{dir_name}!="", RUN+="/usr/bin/systemd-mount --umount /media/%E{dir_name}", RUN+="/bin/rmdir /media/%E{dir_name}"
LABEL="media_by_label_auto_mount_end"
```

### 系统启动后蓝灯
写入 `/etc/rc.local`，稍加修改可自定义颜色。
```
# 系统启动后蓝灯
echo 1 > /sys/class/leds/onecloud:blue:alive/brightness
echo 0 > /sys/class/leds/onecloud:green:alive/brightness
echo 0 > /sys/class/leds/onecloud:red:alive/brightness
```