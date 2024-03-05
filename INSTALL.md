基于官方Armbian源码编译。
感谢hzyitc等开发者为玩客云添加官方源码支持并修复了多项Bug  
https://github.com/hzyitc/armbian-onecloud  


系统特点：支持HDMI、双USB，默认不安装docker可自行安装只需执行 apt install docker.io 命令即可。  

刷入方法：解压固件包，电脑连接玩客云靠近hdmi的USB口，短接刷机触点或者按住复位键的同时给玩客云通电，即可使用Aml Burn Tool软件直接烧录固件至玩客云。  
初始账号密码  root   1234  

(特别注意：USB Burning Tool 请使用2.1.6.8版本，其他版本可能出现超时等报错）  


刷机包下载地址：https://github.com/hzyitc/armbian-onecloud/releases 注意后缀带Burn的才是直刷包，其他都是USB启动包。  

Ubuntu22.04(jammy)   
Debian12(bookworm)  

