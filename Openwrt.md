🟦安装 Armbian 后

🔵更新软件（非必要）

apt-get update && apt-get upgrade

🔵安装 Docker

apt install docker.io

🔵打开网卡混杂模式

ip link set eth0 promisc on

🔵创建网络

docker network create -d macvlan --subnet=192.168.1.0/24 --gateway=192.168.1.1 -o parent=eth0 macnet

🔘[↑自己根据 玩客云 所在网段修改，如：玩客云IP:192.168.2.175，则192.168.1.0/24 改成 192.168.2.0/24，192.168.1.1改成主路由地址]

🔵拉取 OpenWRT 镜像

docker pull xuanaimai/onecloud:21-09-15

🔵创建容器

docker run -itd --name=OneCloud --restart=always --network=macnet --privileged=true xuanaimai/onecloud:21-09-15 /sbin/init

🔘--name=OneCloud 其中OneCloud是容器名称，可以更改成你想要的，容器名称注意不要和其他容器一样，会冲突

🔵根据主路由 DHCP 分配里找到一个主机名叫 OpenWRT 的，复制它的IPv4 地址粘贴到浏览器就能进入 OpenWRT 了

🔘密码是 password

🟥卸载 （如有安装 Portainer 请忽略）

🔴查看所有容器

docker ps -a

🔘记录下 xuanaimai/openwrt:21-09-15 左边的 CONTAINER ID（容器ID，下面用得到）

🔴设置 容器不自启动 、 停止容器 和 删除容器

docker container update --restart=no [容器ID]

docker stop [容器ID]

docker rm [容器ID]

🔴查看所有镜像

docker images

🔘记录下 xuanaimai/openwrt 21-09-15 右边的 IMAGE ID（镜像ID，下面用得到）

🔴删除镜像

docker rmi [镜像ID]

🔘再次用到此镜像的时候，从 [🔵拉取 OpenWRT 镜像] 这一步开始

🟧其他

🟠作为 单臂路由 时

🔸网络 → 接口 → LAN → 物理设置 → 桥接接口 的 √ 去掉

🔸防火墙 → 自定义规则 → [# iptables -t nat -A POSTROUTING -o pppoe-wan -j MASQUERADE] 前的 [# ] 去掉

🔘如果没有这条规则，请添加 iptables -t nat -A POSTROUTING -o pppoe-wan -j MASQUERADE

🔸如果有使用OpenClash，则 OpenClash → 全局设置 → 基本设置 → 绑定网络接口 选择 pppoe-wan

🔸打开 /etc/resolv.conf ，把 127.0.0.11 修改成 127.0.0.1

🔘此方法非永久，重启后恢复 127.0.0.11

🔘flippy大的方法，在 系统 → 启动项最下方的 本地启动脚本 添加

cat > /etc/resolv.conf <<EOF

search lan

nameserver 127.0.0.1

options ndots:0

EOF

➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖➖

感谢 lean大 的 OpenWRT 源码：[https://github.com/coolsnowwolf/lede](https://github.com/coolsnowwolf/lede)

感谢 Lienol大 的 OpenWRT 软件包：[https://github.com/Lienol/openwrt-package](https://github.com/Lienol/openwrt-package)

感谢 flippy大 的制作 Docker 版 OpenWRT 镜像工具：[https://www.right.com.cn/forum/thread-958173-1-1.html](https://www.right.com.cn/forum/thread-958173-1-1.html)

感谢 xtwz 的 OpenWRT编译LUCI插件说明：[https://www.right.com.cn/forum/thread-344825-1-1.html](https://www.right.com.cn/forum/thread-344825-1-1.html)

主要根据 xnxy2012 的 K3固件 选取 OpenWRT 软件（21年1月9日的固件）：[https://www.right.com.cn/forum/thread-3127867-1-1.html](https://www.right.com.cn/forum/thread-3127867-1-1.html)

---

上网设备设置

静态分配IP

IP地址最后一位随便设置，但排除1和255，当然也不能和主路由器上的冲突

比如192.168.2.185

子网掩码不变，还是255.255.255.0 (手机没有这个)

网关设置（安卓手机上叫做“路由器"）为我们旁路由的IP地址

DNS可以设置成旁路由的IP地址，也可以使用144.144.144.144之类的DNS服务器
