# Dell Inspiron 14-3000 3467 OpenCore

[![macOS](https://img.shields.io/badge/macOS-Ventura-orange)](https://www.apple.com/macos/ventura/)
[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.2-blue)](https://github.com/acidanthera/OpenCorePkg)

<details>  
<summary><strong>Recent Changes</strong></summary>
</br>
                                                                                                       
**12/02/2024** : Intial Release.
</details>

<details>  
<summary><strong>Hardware Specs</strong></summary>
</br>

| Model            | Dell Inspiron 14 3467                                                                 |
| :--------------- | :------------------------------------------------------------------------------------ |
| Processor        | Intel Core i5-7200U (2C, 4T, 2.5GHz / 2.71GHz)                                        |
| Graphics         | Integrated Intel HD 620                                                               |
| Memory           | 16 GB DDR4 (2 x 8GB DDR4-2133)                                                        |
| Display          | 14" HD (1366 x 768), Non-Touch                                                        |
| Storage          | 256 GB Crucial MX200 SATA SSD                                                         |
| Ethernet         | Realtek RTL 8100                                                                      |
| WLAN + Bluetooth | Intel AX200                                                                           |
| Camera           | 0.9 Megapixel 720p @ 30 FPS                                                           |
| Audio support    | Realtek ALC3246/ALC256, stereo speakers 2Wx2, microphone, combo audio/microphone jack |
| Keyboard         | 6-row, multimedia Fn keys                                                             |
| Battery          | External Li-Ion 4-cell 40 WHr                                                         |

</details>

<details>  
<summary><strong>Hardware Compatibility</strong></summary>

# Hackintosh Checklist

## What's working?

**Working:** check-mark. **Not Working:** bold.&#x20;

**Not Tested:** leave as-is. **Not applicable:** strike-through or delete.&#x20;

### Useful tools and utilities

[Checklist Tools](https://chriswayg.gitbook.io/opencore-visual-beginners-guide/step-by-step/checklist-tools)

### Desktop and General

#### OpenCore Booting

* [x] Correct OS choices shown in OpenCore Menu/GUI
* [ ] Keyboard shortcuts working (see details below in _OpenCore Boot Key Combinations_)
  * CMD+V — verbose mode _(check KeySwap)_
* [x] NVRAM working: [Verifying if you have working NVRAM](https://dortania.github.io/OpenCore-Post-Install/misc/nvram.html#verifying-if-you-have-working-nvram)
  * Apple -> System Preferences -> Startup Disk (uses NVRAM).
* [ ] Security (especially SIP) use _Menu Bar SIP Detector_
* [ ] FileVault (if used)
* [ ] Windows and/or Linux Multi-Boot
* [x] Recovery (macOS) Boot
* [x] Serial Number: ensure that it does not exist elsewhere, [Check Apple Coverage](https://checkcoverage.apple.com/us/en/) _(and not uploaded to Github)_

#### Display

* [x] Display via HDMI
* [ ] ~~Display via DisplayPort~~
* [ ] ~~Display via DVI~~
* [x] Native Resolution
* [x] Refresh rates
* [ ] Multimonitor displays

#### Graphics Acceleration

* [ ] ~~dGPU dedicated GPU~~
  * ~~In _Terminal_: `gfxutil -f GFX0` or check in _IORegistryExplorer_~~
* [x] iGPU internal GPU
  * In _Terminal_: `gfxutil -f IGPU` or check in _IORegistryExplorer_
* [x] QE/CI _(full acceleration requires both Quartz Extreme and Core Image)_
  * Check for transparent menu bar and fast smooth UI
  * Hackintool -> System -> System -> _Quartz Extreme (QE/CI)_
* [x] VDA _(Video Decode Acceleration framework)_
  * _Hackintool -> System -> System -> VDA Decoder_ (should show '_fully supported_')
  * Or use `VDADecoderChecker`
* [x] Metal
  * _System Information_ -> Graphics/Displays -> Metal: Supported
  * _GLView_
  * _Geekbench_ -> Compute -> Metal
* [ ] Intel Quick Sync, H.264 & HEVC (H.265) hardware decoding/encoding
  * _Intel Power Gadget > GFX_ (green line) check while exporting H.264 from FCP-X
* [ ] ~~dGPU hardware acceleration~~

#### Audio

* [x] Audio out (see in _Audio MIDI Setup_)
* [x] Audio in
* [ ] ~~Frontpanel audio connectors~~
* [x] Audio over HDMI
* [x] Audio quality

#### Sleep & Power

Use _Energy Saver > Restore Defaults_

* [x] Check Hibernate Mode (desktop `0`, laptop `3`). In Terminal: `pmset -g | grep hibernatemode`
* [x] Shutdown (from Apple menu)
* [x] Restart (from Apple menu)
* [x] Manual Sleep (Apple menu ->  Sleep)
* [ ] [Press and hold power button for 1.5 seconds](https://support.apple.com/en-us/HT201236), select Sleep
* [x] Auto Sleep (_System Preferences_ -> Energy Saver)
* [ ] Wake by keyboard
* [ ] Wake by mouse/trackpad

#### CPU

* [x] CPU Power Management [Optimizing Power Management](https://dortania.github.io/OpenCore-Post-Install/universal/pm.html#optimizing-power-management)
  * Check with _IORegistryExplorer_
* [x] Temperatures and stability with 100% CPU
  * Use _Prime95_ Torture Test

#### Disk

Test with _AJA System Test Lite or AmorphousDiskMark_

* [ ] ~~NVMe SSD (PCIe Gen3 or Gen4 speeds)~~
* [x] SATA SSD
* [x] TRIM support (_System Information_ -> SATA -> SSD drive)
* [x] USB Drives

#### Sensors

Check with HWMonitorSMC2

* [x] CPU
* [x] GPU
* [x] SSD, NVMe, HD
* [x] Fans

#### Keyboard

* [x] Option/Command correctly mapped in macOS
  * For PC Keyboards swap in: _System Preferences_ -> Keyboard -> Modifier Keys
  * Press _Spacebar_ and the key left of the Spacebar. This should show Spotlight
* [x] Fn keys working (Audio Volume keys, etc.)

#### USB

Check with _USBToolBox_ or _Hackintool_ (shows connection speed)

Test external drive speed with _AJA System Test Lite_

* [x] USB 2 ports
* [x] USB 2 on USB 3 ports
* [ ] USB 3 and 3.1 ports (check transfer speed during copy)
* [ ] ~~USB Type-C ports~~
* [x] SD Card Reader
* [x] Camera (Photo Booth, Facetime, Zoom)
* [ ] ~~Fingerprint reader~~
* [x] DVD Drive

#### ThunderBolt

* [ ] ~~File transfer~~
* [ ] ~~Display~~

#### Ethernet

* [x] Fast Ethernet LAN
* [ ] ~~Gigabit LAN~~
* [ ] ~~2.5GBase-T (especially on Comet Lake and above boards)~~
* [ ] ~~10GBase-T (Aquantia with updated firmware)~~

#### Wifi & Bluetooth

* [x] Wifi function and transmission speed (Option Click -> Wifi menu bar icon -> check Tx Rate)
* [x] Bluetooth devices (trackpad, mouse, keyboard, headset)
* [ ] AirDrop (test with iDevices)
* [ ] AirPlay to Mac (macOS Monterey or later, test with iOS 14 or later devices)
  * tap the AirPlay icon on your Apple device to share videos to your Hackintosh
* [ ] Handoff [System requirements for Continuity](https://support.apple.com/en-us/HT204689) and [Use Continuity](https://support.apple.com/en-us/HT204681) which requires macOS Catalina & iOS 13+
* [ ] [Sidecar](https://support.apple.com/en-us/HT210380) requires macOS Catalina or later and a compatible iPad using iPadOS 13 or later.

#### OS Features

* [x] iMessage, FaceTime, App Store, iTunes Store
* [x] DRM support _(iTunes Movies, Apple TV+. Amazon Prime and Netflix, and others - test in Safari. Requires AMD Polaris or newer GPU.)_

### Laptop Specific

additional checks relevant for Notebooks including MacBooks with Legacy Patchers

#### Display

* [ ] Backlight setting
* [ ] ~~Backlight sensor~~
* [ ] Backlight Fn keys

#### Audio

* [x] Internal Speakers
* [x] Internal Microphone
* [x] 3.5 mm Jack Headphones
* [x] 3.5 mm Jack Microphone

#### Sleep & Power

* [x] Sleep by close lid
* [x] Sleep by close lid with external display
* [x] Wake by open lid

#### Battery

* [x] Showing percentage
* [x] Showing capacity/health
  * _coconutBattery_
* [x] Charge plug/unplug detected

#### Sensors

* [x] Battery

#### Keyboard & Trackpad

* [x] Keyboard (possibly PS2 based)
* [x] Brightness and other Fn Keys
* [x] Touchpad basic functions
* [x] Touchpad Gestures

_Location of Checklist:_ [https://github.com/chriswayg/Opencore-Visual-Beginners-Guide/blob/master/step-by-step/hackintosh-checklist.md](hackintosh-checklist.md)

[![CC0](https://i.creativecommons.org/p/zero/1.0/88x31.png)](https://creativecommons.org/publicdomain/zero/1.0/) I make this checklist available under public domain [(CC0)](https://creativecommons.org/share-your-work/public-domain/cc0/)
</details>

<details>  
<summary><strong>Photos</strong></summary>
</br>

</details>

<details>  
<summary><strong> ⚠️ Anti-Piracy Warning / Disclaimer ⚠️ </strong></summary>
</br>

### ⚠️ PIRACY IS NO PARTY! ⚠️

I do not endorse or condone the use of pre-configured Hackintosh Distros because not only they cause unnecessary harm to your machine but it is considered to be a form of **Software Piracy**. Software Piracy is a serious crime according to copyright law and is punishable for up to 10 years in prison.

</details>

<details>  
<summary><strong> ⚠️ Anti-Liability Disclaimer ⚠️ </strong></summary>
</br>

Hackintoshing may be dangerous and can damage your device and I am not responsible for bricked devices, dead devices, thermonuclear war, or you getting fired because your system failed. Please do some research if you have any concerns about hackintoshing before you proceed.

</details>

## Credits

<details>  
<summary><strong>Special Thanks to...</strong></summary>
</br>

- [Acidanthera](https://github.com/acidanthera)
- [Dortania OC guide](https://dortania.github.io/OpenCore-Install-Guide/)
- [CorpNewt's tools](https://github.com/corpnewt)
- [VoodooRMI](https://github.com/VoodooSMBus/VoodooRMI)
