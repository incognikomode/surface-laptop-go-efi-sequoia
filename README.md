# macOS Sequoia on Microsoft Surface Laptop Go

![macOS Sequoia](https://img.shields.io/badge/macOS-Sequoia_15.7.3-brightgreen)
![Surface Laptop Go](https://img.shields.io/badge/Device-Surface_Laptop_Go-blue)

Successfully running **macOS Sequoia** on the **Microsoft Surface Laptop Go** using OpenCore.

---

## Hardware Specifications

- **Device**: Microsoft Surface Laptop Go
- **CPU**: Intel Core i5-1035G1 (Ice Lake, 4C/8T)
- **iGPU**: Intel UHD Graphics G1
- **Display**: 12.4" PixelSense Touch Display
- **Wi-Fi / Bluetooth**: Intel AX201 (Wi-Fi 6)
- **Storage**: NVMe SSD
- **SMBIOS**: MacBook Air (Retina, 13-inch, 2020)

---

## What's Working

- macOS Sequoia booting and installation
- Graphics acceleration
- Display output & rendering
- Keyboard
- Trackpad (basic + gestures)
- Wi-Fi (via `itlwm.kext`)
- Bluetooth
- Audio
- Battery status
- Brightness control
- USB ports
- Most daily functions

---

## Known Issues

- **iGPU Framebuffer Issue** (Main Problem):
  - Mouse cursor appears scrambled / corrupted.
  - Temporary workaround: Use **three-finger pinch to zoom in** slightly — this usually fixes the cursor until next movement.
- Sleep/Wake may be unstable.
- Touchscreen support is limited/untested.
- Occasional graphical glitches with mouse movement.

**Contributions welcome** — feel free to fork and improve the iGPU framebuffer patches (WhateverGreen / device-id).

---

## Installation Guide

### 1. Prepare Windows
- Back up all important data.
- Disable **BitLocker** (Settings → Privacy & security → Device encryption).
- Disable **Secure Boot** and **TPM** in UEFI (highly recommended).

### 2. Enter UEFI/BIOS
1. Fully shut down the Surface Laptop Go.
2. Press and hold the **Volume Up** button.
3. While holding Volume Up, press and release the **Power** button.
4. Release Volume Up when the Surface logo appears.

**In UEFI Settings:**
- **Security** → Disable **Secure Boot**
- Disable **TPM** (if available)
- **Boot** → Set USB first in boot order
- Save & Exit

### 3. Create Bootable USB
1. Create a macOS Sequoia installer USB (using another Mac).
2. Replace the `EFI` folder on the USB with the **prebuilt EFI** from this repo.
3. **Wi-Fi Setup (Important)**:
   - Edit: `EFI/OC/Kexts/itlwm.kext/Contents/Info.plist`
   - Update your Wi-Fi credentials:
     ```xml
     <key>SSID</key>
     <string>YourWiFiName</string>
     <key>Password</key>
     <string>YourPassword</string>
     ```

### 4. Installation
1. Insert the USB and boot from it (hold **Volume Down** + Power or select in UEFI).
