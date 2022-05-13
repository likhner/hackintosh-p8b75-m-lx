# Hackintosh P8B75-M LX

## Hardware

| Type         | Model                                                                                                                                                  |
|--------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| Motherboard  | [ASUS P8B75-M LX](https://www.asus.com/Motherboards/P8B75M_LX/specifications/)                                                                         |
| CPU          | [Intel Core i5-3470](https://ark.intel.com/content/www/us/en/ark/products/68316/intel-core-i53470-processor-6m-cache-up-to-3-60-ghz.html) (Ivy Bridge) |
| Video card   | NVIDIA GeForce GTX 960                                                                                                                                 |
| iGPU*        | Intel HD Graphics 2500                                                                                                                                 |
| Network card | Realtek 8111F-VB-CG                                                                                                                                    |
| Sound card   | VIA VT1708S                                                                                                                                            |

*iGPU is used for IQSV

## Issues

| Issue                                             | Fixable? | Reason                                                          | Fix |
|---------------------------------------------------|----------|-----------------------------------------------------------------|-----|
| No sound adjustment of the video card             | ❌        | Not supported by macOS                                          | ❌   |
| The latest supported version is macOS High Sierra | ❌        | NVIDIA graphics cards and iGPU are no longer supported by macOS | ❌   |
| AppleALC is not supported                         | ❌        | Rare sound card                                                 | ❌   |
| Bad sound quality when using VoodooHDA            | ❌        | Rare sound card                                                 | ❌   |

## OpenCore

### Drivers

| Name                                                                                   | Description                     |
|----------------------------------------------------------------------------------------|---------------------------------|
| [HfsPlus](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi) | Required to display HFS volumes |
| [OpenRuntime](https://github.com/acidanthera/OpenCorePkg/releases/latest)              | Required for NVRAM support      |

### SSDTs

| Name                                        | Description                |
|---------------------------------------------|----------------------------|
| [SSDT-EC-DESKTOP](SSDT/SSDT-EC-DESKTOP.dsl) | Fixes embedded controller  |
| [SSDT-PM](SSDT/SSDT-PM.dsl)                 | Fixes CPU power management |
| [SSDT-SBUS-MCHC](SSDT/SSDT-SBUS-MCHC.dsl)   | Fixes SMBus support        |

### Kexts

| Name                                                                                                                  | Description             |
|-----------------------------------------------------------------------------------------------------------------------|-------------------------|
| [Lilu](https://github.com/acidanthera/Lilu/releases)                                                                  | Universal patcher       |
| [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases/download/v2.2.2/RealtekRTL8111-V2.2.2.zip) | Kext for network card   |
| [USBPorts](EFI/OC/Kexts/)                                                                                             | USB port map            |
| [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases/latest) (_SMCProcessor, SMCSuperIO_)                  | Apple SMC Emulator      |
| [VoodooHDA](https://sourceforge.net/projects/voodoohda/files/latest/download)*                                        | Kext for sound card     |
| [WhateverGreen](https://github.com/acidanthera/whatevergreen/releases/latest)                                         | Video card patcher      |
| [NVIDIA Web](https://gfe.nvidia.com/mac-update)                                                                       | Kext for the video card |
| [NVIDIA CUDA](https://www.nvidia.com/en-us/drivers/cuda/mac-driver-archive/)                                          | Kext for CUDA           |

*In the case of VoodooHDA, you must enable `VoodooHDAEnableHalfMicVolumeFix`, `VoodooHDAEnableHalfVolumeFix`, `VoodooHDAEnableMuteFix` и `VoodooHDAEnableVolumeChangeFix` in the `Info.plist` file
