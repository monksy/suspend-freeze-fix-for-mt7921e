# Suspend/Resume Fix for MediaTek MT7921 Adapter on Kernel 6.11.6-

## Issue
A suspend/resume issue occurs on systems with the MediaTek MT7921 Wi-Fi adapter when running on Kernel 6.11.6-. After suspending, the system fails to resume / freezes and requires a hard reset.

### Solution
1. **Add Kernel Parameter**: `mt7921e.disable_aspm=Y`
   - Add this to the kernel parameters in `/etc/default/grub`.
   - Update GRUB and reboot.

2. **Systemd Services**: Create services to disable Wi-Fi and Bluetooth on suspend and re-enable them on resume.
   - `disable-wifi-bluetooth-on-suspend.service`
   - `enable-wifi-bluetooth-on-resume.service`

#### Files
- `disable-wifi-bluetooth-on-suspend.service`: Disables Wi-Fi and Bluetooth on suspend.
- `enable-wifi-bluetooth-on-resume.service`: Re-enables Wi-Fi and Bluetooth on resume.

* Resuming the device after suspension takes some time, around 30 seconds. Which normally shouldn't take. Additionally, on Hyprland, external monitor sometimes goes into cycle of displaying RGB colors in a sequence, simply unplugging the HDMI cable and plugging it back after succesfull resume solves this issue.

## Acknowledgments
Thanks to [herbiejhopkins](https://bbs.archlinux.org/viewtopic.php?pid=2202200#p2202200) and [seth](https://bbs.archlinux.org/viewtopic.php?pid=2202429#p2202429) on Arch Linux forums. herbiejhopkins came up with the idea of rfkill systemd service and seth with the kernel parameter.
