此库都是我在Github上找到的开源EFI，故，使用中出现的所有问题，本人概不负责。本人只是个搬运工，上面都写的有硬件要求，根据要求自己试用


Hackintosh-Opencore-MAG-MSI--B550M-MORTAR-WIFI
微星(MSI)MAG B550M MORTAR WIFI直击炮

苹果系统

开放核心：0.9.7

苹果系统：14.2.1

SMBIOS：MacPro7,1

规格
成分	模型
中央处理器	AMD R7 3700X
母板	微星(MAG) B550M 迫击炮 WIFI
内存	金银32GB(16G×2) DDR4 3600 CJ​​R C18
音频芯片组	ALCS1200A
图形处理器	讯景RX 590 8G
以太网	RTL8125B 2.5GbE
无线网络和蓝牙	英特尔 WiFi 6 AX200
操作系统盘(nvme)	铠侠 RC10 1TB
什么有效
声音的

苹果ALC ( alcid=11 )

以太网

LucyRTL8125以太网

USB

USBToolBox（需要包含USBToolBox.kext和UTBMap.kext）

如果你有USB问题，你可以用它来生成你自己的USB配置信息

无线网络（不可用）

机场Itlwm

蓝牙

英特尔蓝牙固件

IntelBluetoothInjector.kext 将MaxKernel字段设置为20.99.9(BigSur)

BlueToolFixup.kext和IntelBTPatcher.kext将字段设置MinKernel为21.00.0（蒙特雷或更新版本）

新的 AMD 内核补丁
使能够ProvideCurrentCpuInfo

Kernel -> Quirks -> ProvideCurrentCpuInfo

编辑核心计数补丁以匹配您的 CPU

AMD Vanilla OpenCore或OpenCore 安装指南

找到三个algrey - Force cpuid_cores_per_package

kernel -> Patch -> 0  -> Replace适用于 macOS 10.13、10.14

kernel -> Patch -> 1  -> Replace适用于 macOS 10.15,11.0

kernel -> Patch -> 2  -> Replace适用于 macOS 12.0

B8000000 0000 => B8 <core count> 0000 0000
BA000000 0000 => BA <core count> 0000 0000
BA000000 0090 => BA <core count> 0000 0090
核心计数	十六进制
6核	06
8核	08
12核	0℃
16核	10
32核	20
64核	40
例如：3700X 8 核

B8 08 0000 0000
BA 08 0000 0000
BA 08 0000 0090
请使用OpenCore Configurator或 OC Auxiliary 或 GenSMBIOS 生成自己的 SMBIOS

BIOS
我的BIOS版本是7C94v1E，使用这个BIOS你只需要禁用安全启动。

您可以在这里下载所有 BIOS 。

后请勿使用biso 7C94v1E，above 4G默认开启且无法更改。系统将无法启动。

AMD BIOS 设置

我使用npci=0x3000而不是启用4G以上