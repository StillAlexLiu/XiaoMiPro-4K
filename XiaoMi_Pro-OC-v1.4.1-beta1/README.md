<img src="Docs/img/XiaoMi_Hackintosh_with_text_Small.png" width="934" height="48"/>

[![Build Status](https://travis-ci.com/daliansky/XiaoMi-Pro-Hackintosh.svg?branch=master)](https://travis-ci.com/daliansky/XiaoMi-Pro-Hackintosh) [![release](https://img.shields.io/badge/download-release-blue.svg)](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/releases) [![wiki](https://img.shields.io/badge/support-wiki-green.svg)](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/wiki) [![Chat](https://img.shields.io/badge/chat-tonymacx86-red.svg)](https://www.tonymacx86.com/threads/guide-xiaomi-mi-notebook-pro-high-sierra-10-13-6.242724)
-----

macOS Catalina & Mojave & High Sierra on XiaoMi NoteBook Pro 2017 & 2018

English | [中文](README_CN.md)

## Contents

- [Configuration](#configuration)
- [Current Status in Clover](#current-status-in-clover)
- [Current Status in OpenCore](#current-status-in-opencore)
- [Installation](#installation)
  - [First-time installation](#first-time-installation)
  - [Build](#build)
  - [Upgrade](#upgrade)
- [Improvements](#improvements)
- [FAQ](#faq)
- [Changelog](#changelog)
- [A reward](#a-reward)
- [Credits](#credits)
- [Support and discussion](#support-and-discussion)


## Configuration

| Specifications | Detail                                                  |
| ------------------- | ------------------------------------------- |
| Computer model      | Xiaomi NoteBook Pro 15.6''(MX150/GTX)      |
| Processor           | Intel Core i5-8250U/i7-8550U Processor     |
| Memory              | 8GB/16GB Samsung DDR4 2400MHz              |
| Hard Disk           | Samsung NVMe SSD Controller PM961/PM981    |
| Integrated Graphics | Intel UHD Graphics 620                     |
| Monitor             | BOE NV156FHM-N61 FHD 1920x1080 (15.6 inch) |
| Sound Card          | Realtek ALC298 (layout-id:30/99)           |
| Wireless Card       | Intel Wireless 8265                        |
| SD Card Reader      | Realtek RTS5129/RTS5250S                   |


## Current Status in Clover

- <b>HDMI may not work on macOS 10.15.5+, view [acidanthera/bugtracker#938](https://github.com/acidanthera/bugtracker/issues/938)</b>
- <b>Ethernet may not work on macOS 10.15, view [#256](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/issues/256)</b>
- In macOS 10.15, you need to update [Wireless-USB-Adapter Driver](https://github.com/chris1111/Wireless-USB-Adapter/releases)
  - If you are not using macOS 10.15, it's still recommended to update the driver above
- <b>Discrete graphic card</b> is not working, since macOS doesn't support Optimus technology
  - Have used [SSDT-DDGPU](ACPI/SSDT-DDGPU.dsl) to disable it in order to save power
- <b>Fingerprint sensor</b> is not working
  - Have used [SSDT-USB](ACPI/SSDT-USB.dsl) to disable it in order to save power
- <b>Intel Bluetooth</b> may cause sleep problems and does not support some Bluetooth devices
  - View [Work-Around-with-Bluetooth](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/wiki/Work-Around-with-Bluetooth)
- <b>Intel Wi-Fi (Intel Wireless 8265)</b> could work by additional configurations
  - Buy a USB Wi-Fi dongle or supported wireless card
  - Use [itlwm](https://github.com/zxystd/itlwm) and [HeliPort](https://github.com/zxystd/HeliPort) to drive Intel Wi-Fi
  - ~View [#330](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/issues/330), some test drivers are provided there~
- <b>Realtek USB SD Card Reader (RTS5129)</b> is not working
  - Have used [SSDT-USB](ACPI/SSDT-USB.dsl) to disable it in order to save power
- Everything else works well


## Current Status in OpenCore

- Basically the same with [Current Status in Clover](#current-status-in-clover) section
- Limited theme
- <b>Software in Windows may lose activation due to different hardware UUID generated by OpenCore</b>
  - I am not sure whether it works or not. According to [OpenCore Official Configuration](https://github.com/acidanthera/OpenCorePkg/blob/master/Docs/Configuration.pdf), you can try to inject the original firmware UUID to `PlatformInfo - Generic - SystemUUID` in `/OC/config.plist`
- Should Clean NVRAM after using Clover
  - Press `Space` in OpenCore boot page, and then select `Clean NVRAM` entry


## Installation

### First-time installation

- Please refer to the following installation tutorials
  - [Xiaomi Mi Notebook Pro High Sierra 10.13.6](https://www.tonymacx86.com/threads/guide-xiaomi-mi-notebook-pro-high-sierra-10-13-6.242724)
  - [Xiaomi Mi Notebook Pro MacOS Catalina Installation Guide || ENGLISH](https://bit.ly/34biTqw)
- or video tutorials
  - [Xiaomi NoteBook PRO HACKINTOSH INSTALLATION GUIDE !!!](https://www.youtube.com/watch?v=72sPmkpxCvc)
  - [GUIA HACKINTOSH ESPAÑOL 2020 || Instalación de macOS Catalina Xiaomi Mi Notebook Pro](https://www.youtube.com/watch?v=rfG4sGwhE2g)
- If the trackpad doesn't work during the installation, please plug a wired mouse or a wireless mouse projector before the installation. After the installation completes, open `Terminal.app` and run `sudo kextcache -i /`. Wait for the process ending and restart the device. Enjoy your trackpad!
- Complete EFI packs are available in the [releases](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/releases) page.
 - Please don't clone or download the master branch for daily use.
 
 <img src="Docs/img/README_donot_Clone_or_Download.jpg" width="300px" alt="donot_clone_or_download">
 <img src="Docs/img/README_get_Release.jpg" width="300px" alt="get_release">


### Build

- Build the latest beta EFI by running the following command in Terminal:
```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/daliansky/XiaoMi-Pro-Hackintosh/master/makefile.sh)"
```
- Or run the following command in Terminal:
```
git clone --depth=1 https://github.com/daliansky/XiaoMi-Pro-Hackintosh.git
cd XiaoMi-Pro-Hackintosh
./makefile.sh
```
- To build the latest beta EFI with pre-release kexts, run the following command in Terminal:
```
git clone --depth=1 https://github.com/daliansky/XiaoMi-Pro-Hackintosh.git
cd XiaoMi-Pro-Hackintosh
./makefile.sh --PRE_RELEASE=Kext
```
- When build the latest beta EFI with pre-release kexts, some errors may occur in the building stage. Run the following command in Terminal to ignore errors:
```
./makefile.sh --PRE_RELEASE=Kext --IGNORE_ERR
```


### Upgrade

- A complete replacement of `BOOT` and `CLOVER`(or `OC`) folders is required. Delete these two folders and copy them from the [release pack](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/releases).
- You can also update Clover EFI by running the following command in Terminal:

```bash
bash -c "$(curl -fsSL https://raw.githubusercontent.com/daliansky/XiaoMi-Pro-Hackintosh/master/install.sh)"
```


## Improvements

- Use [ALCPlugFix](ALCPlugFix) to fix unworking jack after replug
- Use [DVMT_and_0xE2_fix](BIOS/DVMT_and_0xE2_fix) to set DVMT to 64mb and unlock CFG
- Use [xzhih](https://github.com/xzhih)'s [one-key-hidpi](https://github.com/xzhih/one-key-hidpi) to improve quality of system UI
  - Support 1440x810 HiDPI resolution
  - On macOS > 10.13.6, to enable higher HiDPI resolution (<1600x900), you need to use [DVMT_and_0xE2_fix](BIOS/DVMT_and_0xE2_fix) to set DVMT to 64mb first
- Use [one-key-cpufriend](one-key-cpufriend) to modify CPU power management


## FAQ

#### My touchpad isn't working after update.

You need to rebuild the kext cache after every system update. Use `Kext Utility.app` or type `sudo kextcache -i /` in `Terminal.app`. Then restart. If this still doesn't work, try to press F9.

#### I can't click to drag files using the trackpad.

Starts from [VoodooI2C v2.4.1](https://github.com/alexandred/VoodooI2C/releases/tag/2.4.1), the click down action is emulated to force touch, which causes the failure of click down and drag gestures. You can turn off `Force Click` in `SysPref - Trackpad` or choose `three finger drag` in `SysPref - Accessibility - Mouse & Trackpad - Trackpad Options`.

#### My screen turns to black and has no response during the updating process.

If you have black screen for five minutes and get no response from the device, please force restart your laptop(Long press power button) and choose `Boot macOS Install from ~` entry.

#### My device is locked by `Find My Mac` and can't be booted, what should I do now?

For Clover users, press `Fn+F11` when you are in Clover boot page. Then Clover will refresh `nvram.plist`, and lock message should be removed.  
For OC users, press `Esc` to enter the boot menu during startup. Then, press `Space` key and choose `Clean NVRAM`.

#### [Clover] I opened the `FileVault`, and I can't find macOS partition in Clover boot page, how can I solve it?

It is not recommended to open `FileVault`. You can press Fn + F3 in the Clover boot page and choose the icon with `FileVault`. Then you can boot in the system and close `FileVault`.

#### [Clover] I can't boot in Windows/Linux by using Clover, but able to boot by press F12 and select OS.

Many people met this problem by using the new version of `AptioMemoryFix.efi`. A workaround is to delete `AptioMemoryFix.efi` in `/CLOVER/drivers/UEFI/` and replace it with the old version provided in [#93](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/issues/93).

Also make sure `Sandbox` and `Hyper-V` functions in Windows 10 are disabled.

#### [OC] How to skip the boot menu and automatically boot into the system?

First, in macOS, open `SysPref - Startup Disk`. Choose the target system.  
Then, open `/EFI/OC/config.plist`, and turn off `ShowPicker`.  
When you want to switch OS, press `Esc` during startup to call the boot menu.

### Please refer to detailed FAQ in [wiki FAQ](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/wiki/FAQ).


## Changelog

You can view [Changelog](Changelog.md) for detailed information.


## A reward

All the project is made for free, but you can reward me if you want.

| Wechat                                                     | Alipay                                               |
| ---------------------------------------------------------- | ---------------------------------------------------- |
| ![wechatpay_160](http://7.daliansky.net/wechatpay_160.jpg) | ![alipay_160](http://7.daliansky.net/alipay_160.jpg) |


## Credits

- Thanks to [Acidanthera](https://github.com/acidanthera) for providing [AppleALC](https://github.com/acidanthera/AppleALC), [AppleSupportPkg](https://github.com/acidanthera/AppleSupportPkg), [HibernationFixup](https://github.com/acidanthera/HibernationFixup), [Lilu](https://github.com/acidanthera/Lilu), [NVMeFix](https://github.com/acidanthera/NVMeFix), [OcBinaryData](https://github.com/acidanthera/OcBinaryData), [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg), [VirtualSMC](https://github.com/acidanthera/VirtualSMC), [VoodooInput](https://github.com/acidanthera/VoodooInput), [VoodooPS2](https://github.com/acidanthera/VoodooPS2), and [WhateverGreen](https://github.com/acidanthera/WhateverGreen).
- Thanks to [apianti](https://sourceforge.net/u/apianti), [blackosx](https://sourceforge.net/u/blackosx), [blusseau](https://sourceforge.net/u/blusseau), [dmazar](https://sourceforge.net/u/dmazar), and [slice2009](https://sourceforge.net/u/slice2009) for providing [Clover](https://github.com/CloverHackyColor/CloverBootloader).
- Thanks to [daliansky](https://github.com/daliansky) for providing [OC-little](https://github.com/daliansky/OC-little).
- Thanks to [FallenChromium](https://github.com/FallenChromium), [jackxuechen](https://github.com/jackxuechen), [Javmain](https://github.com/javmain), [johnnync13](https://github.com/johnnync13), [Menchen](https://github.com/Menchen), [Pasi-Studio](https://github.com/Pasi-Studio), [qeeqez](https://github.com/qeeqez), and [Bat.bat](https://github.com/williambj1) for valuable suggestions.
- Thanks to [hieplpvip](https://github.com/hieplpvip) and [syscl](https://github.com/syscl) for providing sample of DSDT patches.
- Thanks to [RehabMan](https://github.com/RehabMan) for providing [EAPD-Codec-Commander](https://github.com/RehabMan/EAPD-Codec-Commander), [EFICheckDisabler](https://github.com/RehabMan/hack-tools/tree/master/kexts/EFICheckDisabler.kext), [OS-X-Clover-Laptop-Config](https://github.com/RehabMan/OS-X-Clover-Laptop-Config), [OS-X-Null-Ethernet](https://github.com/RehabMan/OS-X-Null-Ethernet), and [SATA-unsupported](https://github.com/RehabMan/hack-tools/tree/master/kexts/SATA-unsupported.kext).
- Thanks to [VoodooI2C](https://github.com/VoodooI2C) for providing [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C).
- Thanks to [zxystd](https://github.com/zxystd) for providing [IntelBluetoothFirmware](https://github.com/zxystd/IntelBluetoothFirmware).

### For more detail, please go to [Reference page](https://github.com/daliansky/XiaoMi-Pro-Hackintosh/wiki/References).


## Support and discussion

- Mi Notebooks supported by other projects:
  - [Mi-Gaming-Laptop](https://github.com/johnnync13/XiaomiGaming) by [johnnync13](https://github.com/johnnync13)
  - [Mi-NB-Air-125-6y30](https://github.com/johnnync13/EFI-Xiaomi-Notebook-air-12-5) by [johnnync13](https://github.com/johnnync13)
  - [Mi-NB-Air-125-7y30](https://github.com/influenist/Mi-NB-Gaming-Laptop-MacOS) by [influenist](https://github.com/influenist)
  - [Mi-NB-Air-133-Gen1](https://github.com/johnnync13/Xiaomi-Notebook-Air-1Gen) by [johnnync13](https://github.com/johnnync13)
  - [Mi-NB-Air-133-2018](https://github.com/johnnync13/Xiaomi-Mi-Air) by [johnnync13](https://github.com/johnnync13)

- tonymacx86.com:
  - [[Guide] Xiaomi Mi Notebook Pro High Sierra 10.13.6](https://www.tonymacx86.com/threads/guide-xiaomi-mi-notebook-pro-high-sierra-10-13-6.242724)

- QQ:
  - 247451054 [小米PRO黑苹果高级群](http://shang.qq.com/wpa/qunwpa?idkey=6223ea12a7f7efe58d5972d241000dd59cbd0260db2fdede52836ca220f7f20e)
  - 137188006 [小米PRO黑苹果](http://shang.qq.com/wpa/qunwpa?idkey=c17e190b9466a73cf12e8caec36e87124fce9e231a895353ee817e9921fdd74e)
  - 689011732 [小米笔记本Pro黑苹果](http://shang.qq.com/wpa/qunwpa?idkey=dde06295030ea1692d6655564e392d86ad874bd0608afd7d408c347d1767981b)