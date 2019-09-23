WirelessCrackTools for Android(arm+bcm4329/4330)

此目录下的zip文件为无线破解命令行工具卡刷包，以md5为后缀名的文件为这些文件的md5值比对表

安装:通过第三方recovery卡刷安装WirelessCrackTools-Installer.zip , wpa_cli-v0.8-Installer.zip 或 wpa_cli-v2.1-Installer.zip

卸载:通过第三方recovery卡刷安装WirelessCrackTools-Uninstaller.zip

WirelessCrackTools-Installer.zip工具包中包含aircrack-ng,reaver,wash,pixiewps,iwconfig,macchanger等32个用于无线破解的命令行工具
wpa_cli-Installer.zip工具包中包含wpa_cli客户端程序，它与wpa_supplicant服务端程序关联使用
上述卡刷工具包安装完毕后，重启系统，自行下载并安装termux(5.0+)之类的终端模拟器，便可以使用这些命令行工具了

注意：若手机的网卡芯片不是bcm4329或bcm4330型号的，那么抓包的操作将不被支持，但跑包操作可以用aircrack-ng这个命令
安装该工具包的手机务必拥有root权限，安卓系统版本务必高于4.0，尽可能选用网卡芯片符合以上要求的手机，如:魅族2，Nexus 7等！

## Aircrack-ng
> Aircrack-ng是一个与802.11标准的无线网络分析有关的安全软件，主要功能有：网络侦测，数据包嗅探，WEP和WPA/WPA2-PSK破解。Aircrack-ng可以工作在任何支持监听模式的无线网卡上并嗅探802.11a，802.11b，802.11g的数据。

## 先决条件

 1. 与WiFi芯片组的设备固件和驱动程序，支持监听模式

*截至2016年初，只有大众市场兼容的设备有专用的Broadcom 4329或4330（博通WiFi芯片组的三星Galaxy S1、三星Galaxy S2，Nexus 7，华为荣耀）。bcmon团队开发了这些芯片的固件和驱动程序。
*否则，去寻找在安卓上支持监听模式的无线USB网卡。

2. 在安卓内核中启用的无线扩展

*这通常是与装载器/内核捆绑在一起的。

3. 监控模式固件和驱动程序装载器

*博通4329：bcmon不会加载CyanogenMod > V7由于BCM4329驱动bcmdhd为Galaxy S1移植。使用[ pwnair ]（http://forum.xda-developers.com/showthread.php？T = 2760170）

*博通4330：使用[应用] bcmon（http://bcmon.blogspot.com/）（原作者不再维护该项目）负载监听模式的固件和驱动程序。

*无线USB网卡支持监听模式：这完全取决于你的无线USB适配器，是出于对这个自述范围。您将需要找到并建立驱动程序，以及您的内核源码。否则，你可能会面临的文件格式不匹配的问题。作为Android内核是Linux内核，毕竟，你应该成功的编写Linux驱动源的驱动程序。要么找到一个好的如何编写你的USB无线网卡驱动程序上定义的Android ROM，注意引导使用chroot的Ubuntu或Kali作为替代制作纯Android驱动程序。

## 运行

检查你的无线网卡状态 (应该工作在监听模式):
```
iwconfig
```

检查Airodump是否可以运行:
    `airodump-ng wlan0`

# 相关文档

## Aircrack-ng官方文档
> 使用说明文档可以在这里找到 http://www.aircrack-ng.org

概述

reaver进行暴力破解接入点的WiFi保护设置pin码。

一旦发现WPS-pin，WPA PSK可以恢复和交替AP的无线设置可以重新配置。

而reaver不支持重新配置AP，这可以完成wpa_supplicant一旦WPS PIN是已知的。

描述

reaver目标外部注册功能通过WiFi保护设置规范要求。

接入点提供认证注册与他们目前的无线配置（包括WPA PSK），并接受一个新的配置从注册。

为了作为一个注册认证，注册官必须证明其AP的8位销知识数。管理员可以验证自己随时AP没有任何用户交互。因为WPS协议进行了EAP，注册只需要与AP相关的和不需要任何先验知识的无线加密或配置。

reaver进行暴力破解AP，尝试每个可能的组合为猜测AP的8个数字位。由于密钥都是数字的，有10个（8）（100000000）任何给定的密钥的可能值。然而，由于pin的最后一位是校验和值可以根据以前的7个数字计算，即密钥空间减少到10（10000000）可能的值。

密钥空间进一步由于WPS认证协议削减销减少半和半独立的验证。这意味着，有10个（10000）可能的值为前4位的key和10 - 3（1000）可能的值为后4位的key，与最后一位数字该key是一个校验和。

reaver分别暴力破解前4位和后4位pin，这意味着整个对于WPS密码的密钥空间，可在11000内完成。

reaver可以测试速度针数完全是有限的速度，AP可以处理WPS的要求。一些AP够快一个key可以测试每一秒，其他人都比较慢，只允许一个key每十秒。统计学，它只需要一半的时间，以猜测正确的引脚数。

已知错误

	一些驱动不能很好的支持reaver(在维基上查找最新的驱动列表)

Reaver的用法（无注释）

通常，reaver只需要接口名称和目标AP的BSSID参数：

#reaver -i mon0 -b 00:01:02:03:04:05

#reaver -i mon0 -b 00:01:02:03:04:05 -vv

#reaver -i mon0 -b 00:01:02:03:04:05 -c 11 -e linksys

#reaver -i mon0 -b 00:01:02:03:04:05 --dh-small

#reaver -i mon0 -b 00:01:02:03:04:05 --fixed

#reaver -i mon0 -b 00:01:02:03:04:05 --mac=AA:BB:CC:DD:EE:FF

#reaver -i mon0 -b 00:01:02:03:04:05 -t 2

#reaver -i mon0 -b 00:01:02:03:04:05 -d 0

#reaver -i mon0 -b 00:01:02:03:04:05 --lock-delay=250

#reaver -i mon0 -b 00:01:02:03:04:05 -T .5

#reaver -i mon0 -b 00:01:02:03:04:05 --nack

#reaver -i mon0 -b 00:01:02:03:04:05 --eap-terminate

#reaver -i mon0 -b 00:01:02:03:04:05 --fail-wait=360

Wash的用法

	Wash是一款用于探查开启了WPS功能的AP的工具。它可以从一个网卡接口的进行扫描： 

		# wash -i mon0 

	或者它可以扫描一个pcap文件列表：

		# wash -f capture1.pcap capture2.pcap capture3.pcap

	Wash只会显示支持WPS的接入点。wash显示每个下列信息发现接入点：

		BSSID		目标AP的BSSID 
		Channel		目标AP的信道,在AP的信标分组指定
		WPS Version	目标AP支持的WPS版本
		WPS Locked	目标AP的WPS锁定状态,在AP的信标分组报告
		ESSID		目标AP的ESSID 

	默认情况下，wash将执行一个被动的调查。然而，wash可以被指示发送探头请求给每一个AP，以获得更多关于AP的信息：

		# wash -i mon0 --scan

	通过发送探针请求, wash将响应来自每一个AP的探测请求. 在对AP进行WPS探查后, 我们将收集到关于AP的一些WPS信息，通常包含制作、模型，和版本数据。该数据存储在数据库中的reaver.db调查统计表。

	reaver.db SQLite数据库包含三个表：

		history		此表记录了攻击历史，包括完成百分比和WPA密钥.
		survey		此表是wash每次执行AP破解时重新写入细节信息
		status		此表是用来表示wash/reaver的总体状况
