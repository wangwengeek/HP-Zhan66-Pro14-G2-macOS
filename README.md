# HP-Zhan66-Pro14-G2-macOS

This repository provides Open Core configuration files for HP Zhan66 Pro14 G2. 

[![release](https://img.shields.io/badge/下载-release-blue.svg)](https://github.com/chiccheung/HP-Zhan66-Pro14-G2-macOS/releases) 

## 电脑配置

| 规格     | 详细信息 |
| -------- | ---------------------------------------- |
| 电脑型号 | HP-Zhan66 Pro 14 G2 |
| 处理器 | Intel i5-8265U |
| 内存     | Kingston 8GB DDR4 2400MHz |
| 硬盘     | SK hynix 512GB NVMExpress |
| 集成显卡 | Intel UHD Graphics 620 Whiskey Lake （8086:3EA0） |
| 独立显卡 | Nvidia MX250 |
| 显示器   | 内建显示器 13.9 - 英寸 (1920 x 1080) |
| 声卡     | Realtek ALC236  |
| 网卡     | Wireless USB Network Card |


## 详情

<b>系统版本：macOS Catalina 10.15.1 (19B88) ｜ Open Core 版本：0.5.2</b>

<b>正常工作项说明</b>

- boot-args: `-v` 请按需选择是否保留
- <b>亮度调节按键 FN+F3 | FN+F4</b>
- 可使用[HIDPI](https://github.com/chiccheung/HP-Zhan66-Pro14-G2-macOS/tree/master/HIDPI)开启高清分辨率支持
-  RtWlanU1827.kext & RtWlanU.kext <b>USB无线网卡驱动</b>
   - 参阅：[Wireless-USB-Adapter-Clover](https://github.com/chris1111/Wireless-USB-Adapter-Clover) 
   - 默认已放置以上USB网卡驱动，但仍需安装上述驱动，否则状态栏不显示Wi-Fi图标。
   - 运行后会在EFI目录下创建Clover文件夹，请手动删除。

<b>不正常工作项说明</b>

- 独立显卡
  - 已注入设备属性 `disable-external-gpu` 禁用此设备减少电量消耗
- 读卡器
- 指纹传感器
- Intel 无线网卡&蓝牙
- SystemSerialNumber & MLB 请在config.plst相关条目下自行添加，以正常使用 App Store & iMessage
  - 参阅：[精解OpenCore(2019.10.5).pdf](https://github.com/chiccheung/HP-Zhan66-Pro14-G2-macOS/tree/master/Docs/oc%E9%85%8D%E7%BD%AE%E5%B8%AE%E5%8A%A9%E8%AF%B4%E6%98%8E)
  - 工具：[macinfo](https://github.com/acidanthera/MacInfoPkg/releases)
- <b>首次开机触摸板不可用，清除缓存后重启</b>
  - 常用命令如下
  - 挂载为可写模式 : `sudo mount -uw /`
  - 重启 Finder : `killall Finder`
  - 重建缓存 : `sudo kextcache -i /`

## 资料

-  Open Core
   - 参阅：[OpenCorePkg](https://github.com/acidanthera/OpenCorePkg)
   - 参阅：[OpenCorePkg 中文资料](https://github.com/chiccheung/HP-Zhan66-Pro14-G2-macOS/tree/master/Docs)

-  ACIP hotpatch 修补
   - 参阅：[OC-little By 宪武](https://github.com/chiccheung/HP-Zhan66-Pro14-G2-macOS/tree/master/Docs/OC-%E9%83%A8%E4%BB%B6%E8%A1%A5%E4%B8%81)
   - 感谢 <b>@宪武</b> 重写电池部分hotpatch，并对各项配置进行排错

## 许可证声明

- Copyright (c) 2016-2017, The HermitCrabs Lab
- Copyright (c) 2016-2019, Download-Fritz
- Copyright (c) 2017-2019, savvas
- Copyright (c) 2016-2019, vit9696
