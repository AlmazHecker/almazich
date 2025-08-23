---
title: "How to Root Android Device"
date: 2025-08-23T06:22:46.645Z
tags: ["Android", "Root"]
draft: false
---

**Prerequisites**

1. Install Magisk from official releases: [Magisk GitHub](https://github.com/topjohnwu/Magisk/releases)
2. Install Android SDK platform-tools (we specifically need `fastboot.exe`)

**Terminology**

- **ROM** – Refers to firmware images, not true read-only memory.
- **Recovery ROM** – OS image flashed via recovery partition, usually packaged as a single archive (ZIP, payload.bin) for OTA updates or sideloads.
- **Fastboot ROM** – Complete OS image for flashing via fastboot, with all partitions separated (boot, system, vendor, userdata, etc.) for full or selective flashing.

**Installation Instructions**

1. Download the Fastboot ROM for your device. The OS version must match your current firmware. I specifically download from [here](https://miuirom.org/)
2. Extract `boot.img` from the Fastboot ROM, copy to your phone and patch it with Magisk. The patched image and its path will be displayed in the terminal.
3. Copy the patched image to your PC, turn off your phone, and boot into Fastboot Mode.
4. Flash the patched boot image:

   ```
   fastboot flash boot <magisk_patched>.img
   ```

   Replace `<magisk_patched>` with the path to your patched image.

- **Note:** If you flashed `boot.img` but Magisk did not gain root access, repeat steps 2–4 using `init_boot.img` instead. Flash it with:

```
  fastboot flash init_boot <magisk_patched>.img
```

5. Restart the phone and open the Magisk app. If the Superuser tab is available, you have root access. Otherwise, patch and flash init_boot.img as described above

**Troubleshooting**

- If `fastboot` says **“waiting for devices”**:

- Try a different USB cable or port.
- Check that drivers are installed.
- Open **Device Manager** on Windows and verify there's no warning icon on your device.
- If a warning icon appears, install proper Fastboot drivers.

- Example: On my device, ADB recognized the phone but fastboot didn’t. Installing the correct Fastboot drivers fixed it. Reference: [Beebom Fastboot Drivers Guide](https://beebom.com/fastboot-not-detecting-device-windows-10/)
