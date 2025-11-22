---
title: "Flashing Xiaomi Fastboot ROM"
date: 2025-11-22T04:39:33.134Z
tags: ["Android", "Firmware", "Fastboot"]
draft: false
---

**Prerequisites**

1. Download the Fastboot ROM for your device.
2. Install Android SDK platform-tools (`fastboot.exe` must be in system PATH).
3. Boot the device into Fastboot Mode (**Volume Down + Power** or `adb reboot fastboot`).

**Terminology**

- **Anti-Rollback** – Prevents flashing older firmware. Check with: `fastboot getvar anti`

- **Fastboot ROM** – Complete OS image with separate partitions (boot, system, vendor, userdata, etc.).

**Flashing Instructions**

1. Extract the Fastboot ROM to a folder on your PC.

2. Boot the device into Fastboot Mode.

3. Connect via USB and verify detection:

   ```
   fastboot devices
   ```

   Your device ID must appear. If it doesn't, check out [Troubleshooting](#troubleshooting)

4. Run the provided script or flash manually:

   - `flash_all.bat` – resets everything
   - `flash_all_except_storage.bat` – resets partitions but preserves user data
   - `flash_all_lock.bat` – resets everything + locks bootloader

   Example for full reset with unlocked bootloader:

   ```
   flash_all.bat
   ```

5. Device should automatically reboot. If it didn't run `fastboot reboot` or Hold **Power** button

## **Troubleshooting**

- If `fastboot devices`reports **waiting for devices**:

  - Check Device Manager for issues.
  - Verify drivers are installed: [USB Drivers](https://developer.android.com/studio/run/win-usb)
  - Change USB cable/port.

- If the script runs but does nothing:

  - Ensure `fastboot.exe` is in PATH.
  - Verify the device anti version ≤ firmware anti version.

- If anti-rollback validation fails, it can be manually bypassed by editing scripts, but this risks bricking the device.
