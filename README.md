# Dell Latitude 5480 (i5-8265U) OpenCore EFI

macOS 黑苹果 OpenCore 引导文件，适用于 **Dell Latitude 5480 (i5-8265U)**。

## 电脑配置

| 组件 | 详细信息 |
|------|---------|
| 电脑型号 | Dell Latitude 5480 |
| 处理器 | Intel Core i5-8265U (Whiskey Lake) |
| 集成显卡 | Intel UHD Graphics 620 |
| 声卡 | Realtek ALC236 (layout-id=11) |
| 有线网卡 | Realtek RTL8100 PCIe GBE |
| 无线网卡 | Broadcom BCM94360CS2（已更换，原装 Intel AC 8265 不可驱）|
| 触摸板 | I2C HID (VoodooI2C 中断模式) |
| 目标系统 | macOS Tahoe 26.0 (Sequoia) |
| SMBIOS | MacBookPro15,2 |

## 功能状态

### ✅ 正常工作
- CPU 变频与电源管理
- Intel UHD 620 核显硬件加速
- 声卡（AppleALC, layout-id=11）
- WiFi（Broadcom BCM94360CS2 + OCLP Root Patch）
- 蓝牙（BrcmPatchRAM3 + BlueToolFixup + OCLP Root Patch）
- 有线网卡（RealtekRTL8100）
- USB 端口（USBPorts.kext 全端口映射）
- 电池电量显示（SMCBatteryManager）
- 亮度快捷键
- 触摸板手势（VoodooI2C 中断模式 + SSDT-GPI0）
- 睡眠/唤醒（SSDT-PTSWAK + SSDT-GPRW + SSDT-EXT4-WakeScreen）
- 合盖睡眠（SSDT-LIDpatch）
- iServices（需自行生成唯一序列号）

### ⚠️ 需要额外操作
- WiFi/蓝牙：首次安装后必须在 macOS 内运行 **OCLP → Post-Install Root Patch → Broadcom WiFi**，重启后生效
- USB：如端口映射不准确，需用 USBToolBox 重新映射

### ❌ 不可用
- 指纹识别（无解）
- AirDrop（博通卡 OCLP 补丁下有限支持）

## Kexts 列表

| Kext | 用途 |
|------|------|
| Lilu | 内核补丁框架 |
| VirtualSMC | SMC 仿真器 |
| WhateverGreen | 核显补丁 |
| AppleALC | 声卡补丁 |
| BrightnessKeys | 亮度快捷键映射 |
| RealtekRTL8100 | 有线网卡驱动 |
| RestrictEvents | 系统限制绕过 |
| SMCBatteryManager | 电池状态 |
| SMCDellSensors | Dell 传感器（风扇/温度）|
| SMCLightSensor | 光线传感器 |
| SMCProcessor | CPU 温度监控 |
| SMCSuperIO | 风扇转速 |
| VoodooI2C + VoodooGPIO + VoodooI2CServices + VoodooInput | I2C 触摸板驱动 |
| VoodooI2CHID | I2C HID 设备 |
| VoodooPS2Controller + VoodooPS2Keyboard | PS/2 键盘驱动 |
| AMFIPass | AMFI 绕过（OCLP 补丁依赖）|
| IOSkywalkFamily | WiFi 框架（OCLP 补丁依赖）|
| IO80211FamilyLegacy + AirPortBrcmNIC | 博通 WiFi 驱动 |
| BlueToolFixup | 蓝牙修复 |
| BrcmFirmwareData | 博通固件数据 |
| BrcmPatchRAM3 | 博通 RAM 补丁 |
| NVMeFix | NVMe 电源管理 |
| USBPorts | USB 端口映射（10 端口）|

## SSDT 列表

| SSDT | 用途 |
|------|------|
| SSDT-ALSD | 光感传感器 |
| SSDT-SBUS | 系统总线 |
| SSDT-EC | 仿冒嵌入式控制器 |
| SSDT-GPI0 | 启用 GPIO（I2C 触摸板中断模式）|
| SSDT-MCHC | 内存控制器 Hub |
| SSDT-PMC | 300 系列主板 NVRAM 支持 |
| SSDT-PLUG | CPU 电源管理 |
| SSDT-PNLF | 背光控制 |
| SSDT-RTCAWAC | RTC/AWAC 时钟修复 |
| SSDT-USBX | USB 电源属性 |
| SSDT-XOSI | OS 接口欺骗 |
| SSDT-GPRW | USB 唤醒修复 |
| SSDT-PTSWAK | 睡眠唤醒修复（六补丁）|
| SSDT-EXT4-WakeScreen | 唤醒后屏幕亮起 |
| SSDT-LIDpatch | 合盖睡眠修复 |

## BIOS 设置

| 选项 | 设置 |
|------|------|
| VT-x | Enabled |
| VT-d | Enabled |
| Above 4G Decoding | Enabled |
| Secure Boot | Disabled |
| Fast Boot | Disabled |
| SATA Operation | AHCI |

## 安装步骤

1. 将 EFI 文件夹复制到 U 盘的 EFI 分区
2. 从 U 盘启动 OpenCore
3. 安装 macOS
4. 安装完成后，将 EFI 从 U 盘复制到硬盘 EFI 分区
5. **重要**：进入系统后运行 OCLP → Post-Install Root Patch → Broadcom WiFi → 重启
6. 验证 WiFi、蓝牙、USB、触摸板是否正常

## 参考项目

| 项目 | 说明 |
|------|------|
| [daggeryu/DELL-Inspiron_5488_5480_5580_5482_5582_Hackintosh](https://github.com/daggeryu/DELL-Inspiron_5488_5480_5580_5482_5582_Hackintosh) | Dell 5480/5488 系列黑苹果参考配置，本项目的 USB 端口映射（USBPorts.kext）和睡眠唤醒 SSDT（GPRW, PTSWAK, EXT4-WakeScreen, LIDpatch）来源于此 |
| [Acidanthera/OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) | OpenCore 引导程序 |
| [Acidanthera/Lilu](https://github.com/acidanthera/Lilu) | 内核补丁框架 |
| [Acidanthera/WhateverGreen](https://github.com/acidanthera/WhateverGreen) | GPU 补丁 |
| [Acidanthera/VirtualSMC](https://github.com/acidanthera/VirtualSMC) | SMC 仿真器 |
| [Acidanthera/AppleALC](https://github.com/acidanthera/AppleALC) | 声卡补丁 |
| [Acidanthera/BrcmPatchRAM](https://github.com/acidanthera/BrcmPatchRAM) | 博通蓝牙固件注入 |
| [Acidanthera/OCLP](https://github.com/acidanthera/OpenCore-Legacy-Patcher) | OpenCore Legacy Patcher（博通 WiFi 根补丁）|
| [VoodooI2C/VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) | I2C 触摸板驱动 |
| [Acidanthera/VoodooPS2](https://github.com/acidanthera/VoodooPS2) | PS/2 键盘驱动 |
| [Mieze/RealtekRTL8100](https://github.com/Mieze/RTL8100) | Realtek 有线网卡驱动 |

## 致谢

- **@daggeryu** - Dell 5480/5488 系列黑苹果参考配置、USB 映射、睡眠唤醒 SSDT
- **@Acidanthera** - OpenCore、Lilu、WhateverGreen、VirtualSMC、VoodooPS2、AppleALC、BrcmPatchRAM、OCLP
- **@VoodooI2C** 及开发团队 - I2C 触摸板驱动
- **@Mieze** - RealtekRTL8100 有线网卡驱动