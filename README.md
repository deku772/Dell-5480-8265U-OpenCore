---
AIGC:
  ContentProducer: '001191110102MAD55U9H0F10002'
  ContentPropagator: '001191110102MAD55U9H0F10002'
  Label: '1'
  ProduceID: '88af3b01-bab1-42cb-9dc9-cd375d5bf874'
  PropagateID: '88af3b01-bab1-42cb-9dc9-cd375d5bf874'
  ReservedCode1: '72d76800-2327-4200-9130-ae47195da186'
  ReservedCode2: '72d76800-2327-4200-9130-ae47195da186'
---

# Dell-5480-8265U-OpenCore

OpenCore EFI for Dell Latitude 5480 (i5-8265U)

## Specs

| Component | Detail |
| --- | --- |
| CPU | Intel Core i5-8265U (Whiskey Lake) |
| GPU | Intel UHD Graphics 620 |
| WiFi | Intel Wireless |
| Ethernet | Realtek RTL8100 |
| Trackpad | I2C HID (VoodooI2C) |
| macOS | Tahoe 26.0 |

## Working

- [x] CPU Power Management
- [x] Intel UHD 620 Graphics Acceleration
- [x] Audio (AppleALC)
- [x] WiFi (AirportItlwm)
- [x] Bluetooth (IntelBluetoothFirmware)
- [x] Ethernet (RealtekRTL8100)
- [x] USB Ports (USBToolBox mapped)
- [x] Battery Status (SMCBatteryManager)
- [x] Brightness Keys
- [x] Sleep/Wake
- [x] iServices

## Partially Working

- [ ] Trackpad Gestures (VoodooI2C polling mode, investigating GPIO interrupt)

## Not Working

- Airdrop (Intel WiFi limitation)

## Kexts

| Kext | Version | Description |
| --- | --- | --- |
| Lilu | | Kernel extension framework |
| VirtualSMC | | SMC emulator |
| WhateverGreen | | GPU patches |
| AppleALC | | Audio patches |
| AirportItlwm | | Intel WiFi |
| IntelBluetoothFirmware | | Intel Bluetooth |
| VoodooI2C | 2.9.1 | I2C trackpad driver |
| VoodooI2CHID | 1.0 | I2C HID satellite |
| VoodooPS2Controller | 2.3.8 | PS/2 keyboard driver |
| RealtekRTL8100 | | Ethernet driver |
| RestrictEvents | | System restrictions patches |
| AMFIPass | | AMFI bypass |
| NVMeFix | | NVMe power management |
| BrightnessKeys | | Brightness key mapping |
| SMCBatteryManager | | Battery status |
| USBToolBox + UTBMap | | USB port mapping |

## BIOS Settings

- VT-x: Enabled
- VT-d: Enabled
- Above 4G Decoding: Enabled
- Secure Boot: Disabled
- Fast Boot: Disabled

## Credits

- [Acidanthera](https://github.com/acidanthera) - OpenCore, Lilu, WhateverGreen, VirtualSMC, VoodooPS2
- [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C) - I2C trackpad driver
- [OpenIntelWireless](https://github.com/OpenIntelWireless) - Intel WiFi & Bluetooth
- [Mieze](https://github.com/Mieze) - RealtekRTL8100