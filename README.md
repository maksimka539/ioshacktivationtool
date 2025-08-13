# 📱 iOS 5–10 Hacktivation Tool

**Author:** [maksimka539](https://github.com/maksimka539)\
**Compatibility:** iOS 5.0 – 10.3.4 (32-bit devices only)\
**Purpose:** Bypass iCloud activation screen using SSH Ramdisk method.

---

## 🧩 What is this?

This tool is designed for **iCloud-locked 32-bit iOS devices** running iOS 5–10.\
It uses an **SSH Ramdisk**, loaded via [Legacy iOS Kit](https://github.com/LukeZGD/Legacy-iOS-Kit), to patch system files and simulate activation.\
No activation files are required — everything is done directly via SSH.

---

## ✅ Supported iOS Versions

| iOS Version | Activation Method                          |
| ----------- | ------------------------------------------ |
| iOS 5–6     | Replace `lockdownd` with patched version   |
| iOS 7–10    | Remove `Setup.app` + patch `MobileGestalt` |

---

## 🛠 Requirements

### 📦 Dependencies

Install the required tools:

**macOS (Homebrew):**

```bash
brew install sshpass libimobiledevice
```

**Linux (APT, for Debian/Ubuntu):**

```bash
sudo apt update
sudo apt install sshpass libimobiledevice-utils
```

Also ensure these are installed:

- `ssh`
- `scp`
- `nc`
- `bash`

---

### 🧰 You will also need

1. **Legacy iOS Kit**\
   Used to create and launch the SSH Ramdisk.\
   → [https://github.com/LukeZGD/Legacy-iOS-Kit](https://github.com/LukeZGD/Legacy-iOS-Kit)

2. **SSH Ramdisk Mode**\
   Enter this mode using Legacy iOS Kit.\
   After launching, the device will be accessible at `127.0.0.1:6414` via SSH.\
   Remember to click **Connect to SSH**.

3. **Mounted Filesystem**\
   Before running the script, make sure the device's filesystems are mounted.\
   In the SSH window, run:

```bash
mount.sh
```

---

## 📁 Folder Structure

```
ios_5_10_hacktivation_tool/
├── hacktivate.sh            # Main script
└── lockdownd                # Required only for iOS 5–6
```

---

## 🚀 Usage Instructions

1. 📥 **Download and unzip the tool:**

```bash
unzip ios_5_10_hacktivation_tool.zip
cd ios_5_10_hacktivation_tool
chmod +x hacktivate.sh
```

2. 🔧 **Run SSH Ramdisk using Legacy iOS Kit**\
   The device must be in **SSH mode** (port 6414).\
   See: [Legacy iOS Kit SSH Ramdisk Guide](https://github.com/LukeZGD/Legacy-iOS-Kit/wiki/SSH-Ramdisk)

3. 🗂 **Connect to SSH and mount filesystems:**

```bash
ssh -p 6414 root@127.0.0.1
mount.sh
```

4. 📌 **Without closing the SSH window**, open a new terminal window, navigate to the folder containing the script, and run it:

```bash
./hacktivate.sh
```

5. ⌨️ **Enter the iOS version** when prompted (e.g., `6.1.3`, `8.4.1`, `9.3.5`).

---

## 🔧 What the Script Does

### For iOS 5–6:

- Replaces `/usr/libexec/lockdownd` with a patched version.
- Reboots the device.
  > The patched `lockdownd` must be placed in the `resources/` folder.

### For iOS 7–10:

- Removes `Setup.app` to hide the activation screen.
- Patches `/private/var/mobile/Library/Caches/com.apple.MobileGestalt.plist` by adding:

```xml
  <dict>
    <key>a6vjPkzcRjrsXmniFsmOdg</key>
    <true/>
  </dict>
```

- Optionally deletes `activation_records`, `data_ark.plist`, and related lockdown files.
- Reboots the device.

After reboot, the device should appear as **activated** in iTunes and 3uTools.

---

## ⚠️ Important Notes

- Works only on **32-bit devices** (iPhone 4, 4s, 5; iPad 2/3/4; iPad mini 1; iPod touch 4/5).
- **Does not** support 64-bit devices (iPhone 5s and newer).
- This **does not remove iCloud lock**, it only bypasses the activation screen.

---

## 💬 Credits & Contact

Author: [**@maksimka539**](https://github.com/maksimka539)\
Credits to [**iPh0ne4s**](https://github.com/iPh0ne4s) for the [**lockdownd**](https://github.com/iPh0ne4s/iOS-5-6-Hacktivation) file.

Feel free to open Issues or Pull Requests for suggestions and improvements.

