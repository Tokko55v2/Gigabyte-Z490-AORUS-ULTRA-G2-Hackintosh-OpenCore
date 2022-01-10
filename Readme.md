# Gigabyte Z490 AORUS ULTRA G2 Hackintosh OpenCore
[![Board](https://img.shields.io/badge/Gigabyte-Z490%20G2-green.svg)](https://www.gigabyte.com/at/Motherboard/Z490-AORUS-ULTRA-G2-rev-1x#kf)
[![BIOS](https://img.shields.io/badge/BIOS-F21-important.svg)](https://www.gigabyte.com/at/Motherboard/Z490-AORUS-ULTRA-G2-rev-1x/support#support-dl-driver)
[![OpenCore Version](https://img.shields.io/badge/OpenCore-0.7.7-cyan.svg)](https://github.com/acidanthera/OpenCorePkg/releases/latest)
[![macOS Monterey](https://img.shields.io/badge/macOS-12.2-white.svg)](https://www.apple.com/macos/monterey/)

## Build Info

In generel I followed the OpenCore [installation Guide](https://dortania.github.io/OpenCore-Install-Guide/). 
* Create a bootable USBStick
  * [Installer Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
* Follow the Comet Lake instructions (config.plist)
* and so on...
### System Specs

| Component           | Details                                                 |
| :-------------------|-------------------------------------------------------- |
| Mainboard           | Gigabyte Z490 Ultra G2                                  |
| BIOS		      | F21 |
| CPU                 | Intel® Core i5 10600K (Comet Lake)          	        |
| RAM                 | 32 GB DDR4 2666 Beast K2 KFY             |
| GPU                 | Radeon RX 580 8GB                   |
| Audio               | Realtek® ALC1220-VB (Layout-id: `28`)                   |
| Ethernet (onboard)  | Intel® I225-V 2.5GbE.|


### BIOS Settings
* Tweak
  * Advanced CPU Settings
    * VT-d: Enabled
    * Intel Speed: Enabled
* Settings
  * IO Ports
    * Above 4G Decoding: Enabled
    * Network Stack Configuration
      * Network Stack: Disabled
* Boot
  * CFGLock: Disabled
  * Window 10 Features: Windows 10
  * CSM: Should be disabled to get rid of legacy code from `DSDT` but unfortunately `Radeon RX 580` does not work with CSM disabled. I have it `enabled`.

### OpenCore Details
* Version: 0.7.7
* Compatible macOS: 10.14 to 12.1
* System Definition: iMac 20,1

### EFI Folder Structure

```
EFI
├── BOOT
│   └── BOOTx64.efi
└── OC
    ├── ACPI
    │   ├── SSDT-AWAC.aml
    │   ├── SSDT-EC-USBX-DESKTOP.aml
    │   ├── SSDT-PLUG-DRTNIA.aml
    │   ├── SSDT-RHUB.aml
    ├── Drivers
    │   ├── HfsPlus.efi
    │   ├── OpenCanopy.efi
    │   └── OpenRuntime.efi
    ├── Kexts
    │   ├── AppleALC.kext
    │   ├── Airportltwm.kext
    │   ├── IntelMausi.kext
    │   ├── Lilu.kext
    │   ├── NVMeFix.kext
    │   ├── USBInjectAll.kext
    │   ├── VirtualSMC.kext
    │   └── WhateverGreen.kext
    ├── OpenCore.efi
    ├── Resources
    │   ├── Font
    │   ├── Image
    │   │   └── Acidanthera
    │   │       ├── Chardonnay
    │   │       ├── GoldenGate
    │   │       └── Syrah
    │   └── Label
    └── config.plist
```

## Installation

If you already have macOS installed but want to perform a clean install, you can either download macOS from the App Store or use [**ANYmacOS**](https://www.sl-soft.de/en/anymacos/). If you have not updated to BigSure for example you can download it from the AppStore. After the download you can find the downloaded macOS in the `Applications` folder.

If you are on Windows or Linux, follow the guide provided by [Dortania](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer)

## EFI Install Guide for OpenCore

I will skip some steps because it could lead to an endless readme. I will point out some important configs that you should be aware of.

* Getting the Intel(R) I225-V Ethernet Controller to work:
  * NOTE: For getting the I225 Controller to work in macOS Monterey, version beta 7 is required at least! - nothing else has to be changes at Monterey.
  * macOS Big Sure need following changes:
    * Enable (un-comment with a `#`) `DeviceProperties`: `#PciRoot(0x0)/Pci(0x1C,0x1)/Pci(0x0,0x0)`
    * Go to `Kernel`: `Patch` and enable `I225-V Patch`.
    * Disable or Delete boot-arg `dk.e1000=0`.

* Create SMBIOS infos for `iMac20,1` to the config.plist and save it.
* Copy the EFI Folder to a FAT32 formatted USB Stick
* Reboot from USB Stick
* Boot macOS
* Continue with installing macOS

## Post-Install
Once you got macOS running copy the EFI Folder from the USB Stick to the EFI Folder to the System.

# Credits and Thank yous
- Acidanthera and Team for the [OpenCore Bootloader](https://github.com/acidanthera/OpenCorePkg)
- Dortania for [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
- TECHNolli [Technolli])(https://www.technolli.com/)