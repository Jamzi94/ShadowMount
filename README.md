# ShadowMount (PS5)
**v1.4 by Jamzi & VoidWhisper**

**ShadowMount** is a fully automated, background "Auto-Mounter" payload for Jailbroken PlayStation 5 consoles. It streamlines the game mounting process by eliminating the need for manual configuration or external tools (such as DumpRunner or Itemzflow). ShadowMount automatically detects, mounts, and installs game dumps from both **internal and external storage**.

**Compatibility:** Supports all Jailbroken PS5 firmwares running **Kstuff v1.6.7**.

---

## 🚀 Key Features

* **Zero-Touch Automation:** No menus, no clicks. ShadowMount scans your storage and installs games automatically.
* **No Extra Apps Required:** Replaces the need for Itemzflow, webMAN, DumpRunner, DumpInstaller, WebSrv, or the Homebrew Store for mounting operations.
* **Automated Asset Management:** Automatically handles assets eliminating the need to copy files through other tools.
* **Hot-Swap Support:** Seamlessly handles unplugging and replugging drives without system instability.
* **Batch Processing:** Capable of scanning and mounting dozens of games simultaneously in seconds.
* **Smart Detection:** Intelligently detects previously mounted games on boot and skips them to ensure zero-overhead startup.
* **Recursive Scanning:** Scans up to 5 levels deep to find games in nested folders.
* **Single-Pass Architecture:** Optimized scanning with no redundant operations.
* **Visual Feedback:**
    * **System Notifications:** Non-intrusive status updates for new installations.
    * **Rich Toasts (Optional):** Graphical pop-ups confirming "Game Installed".
      * *Note: This feature requires `notify.elf`. It is kept as a separate payload for users who prefer a cleaner experience without pop-ups.*

---

## 📂 Supported Paths
ShadowMount performs a **recursive scan** (up to 5 levels deep) of **Internal Storage**, **M.2 SSD**, and **All USB Ports** for the following directory structures:

### Internal Storage
* `/data/homebrew`
* `/data/etaHEN/games`

### Extended Storage (M.2 SSD)
* `/mnt/ext0/homebrew` & `/mnt/ext0/etaHEN/homebrew` & `/mnt/ext0/etaHEN/games`
* `/mnt/ext1/homebrew` & `/mnt/ext1/etaHEN/homebrew` & `/mnt/ext1/etaHEN/games`

### USB Storage (USB0-USB7)
* `/mnt/usb0/homebrew` through `/mnt/usb7/homebrew`
* `/mnt/usb0/etaHEN/games` through `/mnt/usb7/etaHEN/games`

---

## 🛠️ Installation & Usage

**Prerequisites:**
* Jailbroken PS5 Console.
* **Kstuff v1.6.7**
* *Note: etaHEN and Itemzflow are OPTIONAL. ShadowMount works independently.*

### Method 1: Manual Payload Injection (Port 9021)
Use a payload sender (such as NetCat GUI or a web-based loader) to send the files to **Port 9021**.

1.  Send `notify.elf` (Optional).
    * *Only send this if you want graphical pop-ups. Skip if you prefer standard notifications.*
2.  Send `shadowmount.elf`.
3.  Wait for the notification: *"ShadowMount v1.4 by Jamzi & VoidWhisper"*.

### Method 2: PLK Autoloader (Recommended)
Add ShadowMount to your `autoload.txt` for **plk-autoloader** to ensure it starts automatically on every boot.

**Sample Configuration:**
```ini
!1000
kstuff.elf
!1000
notify.elf  ; Optional - Remove this line if you do not want Rich Toasts
!1000
shadowmount.elf
```

---

## 📋 Changelog

### v1.4 (January 2026)
**New Features:**
- ✅ **Recursive Scanning** - Scans up to 5 levels deep to find games in nested folder structures
- ✅ **Single-Pass Architecture** - Eliminated double-scan overhead for faster startup
- ✅ **Extended Storage Paths** - Added `/mnt/ext0/homebrew` and `/mnt/ext1/homebrew`
* `/mnt/ext0/homebrew` & `/mnt/ext0/etaHEN/homebrew` & `/mnt/ext0/etaHEN/games`
* `/mnt/ext1/homebrew` & `/mnt/ext1/etaHEN/homebrew` & `/mnt/ext1/etaHEN/games`

**Optimizations:**
- 🚀 **64KB Copy Buffers** - Increased from 8KB for faster file operations
- 🚀 **Safe String Operations** - Replaced all `strncpy` with `snprintf` to prevent buffer issues
- 🚀 **Improved JSON Parser** - Now handles escaped quotes correctly
- 🚀 **Log Initialization** - Directory created once at startup instead of every log call
- 🚀 **param.json Size Limit** - Capped at 1MB to prevent memory issues

**Bug Fixes:**
- 🔧 **Skip Mounted Games** - Games already mounted via nullfs are now properly skipped
- 🔧 **Cache Validation** - Stale cache entries are now cleaned up automatically
- 🔧 **Root Path Removal** - Removed redundant root paths that caused duplicate/system folder scans

### v1.3 (Original)
- Initial release by VoidWhisper

---

## ⚠️ Notes
* **First Run:** If you have a large library, the initial scan may take a few seconds to register all titles.
* **Large Games:** For massive games (100GB+), allow a few extra seconds for the system to verify file integrity before the "Installed" notification appears.
* **Nested Folders:** Games can now be placed in subfolders up to 5 levels deep (e.g., `/mnt/ext1/homebrew/PS5/Action/MyGame/`)

## Credits
* **Jamzi** - v1.4 Development, Recursive Scanning, Optimizations
* **VoidWhisper** - Original Developer & Logic Implementation (v1.0-v1.3)
* **Special Thanks:**
    * EchoStretch
    * LightningMods
    * john-tornblom
    * PS5 R&D Community

---

[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/voidwhisper)
