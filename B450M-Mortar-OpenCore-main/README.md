# 关于 | About
此EFI专门用于主板B450M MORTAR(MAX)定制，无法保证其他主板的兼容性

This EFI is made for B450M MORTAR(MAX), can not guarantee support with other motherboards.

# ⚠️⚠️⚠️此 EFI 使用注意事项，不看90%扑街⚠️⚠️⚠️

### **1.** 默认config为物理核心数为 `6核` 的AMD CPU使用，如果你是 `4核` 或者 `8核` 及以上的请自行修改，不然无法启动
- 首先，使用任意文本编辑器使用查找功能查找关键词 `Force cpuid_cores_per_package`，一共四个，紧接着找到对应它的键值 `Replace`，将其更改成如下表格
- 
| 核心数 | 数值|
|-|-|
|   4 Core  | `uAQAAAAA` `ugQAAAAA` `ugQAAACQ` `ugQAAAA=`|
|   6 Core  | `uAYAAAAA` `ugYAAAAA` `ugYAAACQ` `ugYAAAA=` (默认)|
|   8 Core  | `uAgAAAAA` `uggAAAAA` `uggAAACQ` `uggAAAA=`|
|   12 Core | `uAwAAAAA` `ugwAAAAA` `ugwAAACQ` `ugwAAAA=`|
|   16 Core | `uBAAAAAA` `uhAAAAAA` `uhAAAACQ` `uhAAAAA=`|

- 举个栗子，我的CPU是5900x，12个物理核心，那么原本的config.plist中 `uAYAAAAA` `ugYAAAAA` `ugYAAACQ` `ugYAAAA=` 分别替换为 `uAwAAAAA` `ugwAAAAA` `ugwAAACQ` `ugwAAAA=`，所以如果你实在看不懂config文本格式，可以直接查找替换这些值

### **2.** 关于 Resizeble BAR 的开启
- 如果你在 BIOS 中开启了 Resizeble BAR，那么你应当调整此项内容，否则无法启动！
- 配置文件默认关闭，所需要调整的键值为 `Booter` -> `Quirks` -> `ResizeAppleGpuBars`
- 和 Windows/Linux 不同，macOS 并不完全支持此功能，其最大限制值是 1GB，对应数值如下表：
- 
|输入|对应值|
|-|-|
-1（默认）|关闭
0|1 MB
1|2 MB
2|4 MB
3|8 MB
4|16 MB
5|32 MB
6|64 MB
7|128 MB
8|256 MB
9|512 MB
10|1 GB

* ResizeAppleGpuBars 建议值如下：
  * -1：关闭
  * 0：1MB（保险值）
  * 8：256MB（传统值）
  * 10：1GB（macOS 支持最大值）
- 可优先尝试 `10`，这么设置的目的是尝试使用 macOS 最大值看看能不能一定程度提升性能；如果遇到休眠问题（表现类似睡了即醒）或开机黑屏的问题，则修改为 `8`；如果问题依旧，可改成 `0`

### **3.** 关于 SIP
- 默认关闭macOS的SIP，这将导致无法直接进入Recovery模式，如有需要自行删除配置文件里的值 `NVRAM` -> `Add` -> `7C436110-AB2A-4BBB-A880-FE41995C9F82` -> `csr-active-config`

# 亮机截图
![](https://github.com/TheStupidNoob/B450M-MORTAR-OpencoreEFI/blob/main/preview.png)
![](https://github.com/tekteq/opencanopy-minimal-theme/blob/main/Preview.png)
