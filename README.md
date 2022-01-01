# Gigabyte M32U

This is truly awesome monitor that basically can be fully controlled
programmatically either over USB (HID device in KVM mode) or using DDC/CI (over HDMI/DP/Type-C).

The vendor codes are equal for HID and DDC/CI, as HID device effectively
encapsulates DDC/CI communication.

This repository contains a fix for [ddcctl (OSX)](https://github.com/kfix/ddcctl]
to allow control various aspects of the monitor.

The change can easily be adapter to [ddccontrol](https://github.com/ddccontrol/ddccontrol)
or [gbmonctl](https://github.com/kelvie/gbmonctl).

This likely applies to all Gigabyte monitors based on Realtek and using OSD Sidekick.

## Example

```bash
# Enable PIP
./bin/release/ddcctl -d 1 -vendor_ext 0x0e0001

# Enable PBP
./bin/release/ddcctl -d 1 -vendor_ext 0x0e0002

# Switch PBP/PIP inputs
./bin/release/ddcctl -d 1 -vendor_ext 0x100001

# Disable PBP/PIP
./bin/release/ddcctl -d 1 -vendor_ext 0x0e0000

# Switch KVM to USB-B
./bin/release/ddcctl -d 1 -vendor_ext 0x690000

# Switch KVM to Type-C
./bin/release/ddcctl -d 1 -vendor_ext 0x690001
```

## Vendor codes

./bin/release/ddcctl -d 1 -vendor_ext 0xXX00YY

| XX   | YY                              |
|------|---------------------------------|
| 0x02 | Black Equalizer: 0x0-0xA (0-10) |
| 0x03 | Color Temperature: 0 - cool, 1 - normal, 2 - warm, 3 - user-defined |
| 0x04 | Color Temperature Red: 0x0-0x64 (0-100) |
| 0x05 | Color Temperature Blue: 0x0-0x64 (0-100) |
| 0x06 | Color Temperature Green: 0x0-0x64 (0-100) |
| 0x07 | Gamma: 0 - off, 1 - 1.8, 2 - 2.0, 3 - 2.2, 4 - 2.4, 5 - 2.6 |
| 0x08 | Color Vibrance: 0x0-0x14 (0-20) |
| 0x0A | Aim Stabilizer: 0 - off, 1 - on |
| 0x0B | Low Blue Light: 0x0-0xA (0-10) |
| 0x0C | Free Sync: 0 - off, 1 - on |
| 0x0D | Super Resolution: 0-4 |
| 0x0E | PBP/PIP Mode: 0 - off, 1 - PIP, 2 - PBP |
| 0x0F | PBP/PIP Source: 0 - HDMI1, 1 - HDMI2, 2 - DP, 3 - Type-C |
| 0x10 | PBP/PIP Switch: use 1 |
| 0x13 | PBP/PIP Audio Switch: use 1 |
| 0x14 | PIP Size: 0 - large, 1 - medium, 2 - small |
| 0x15 | PIP Location: 0 - top-left, 1 - top-right, 2 - bottom-left, 3 - bottom-right |
| 0x18 | Dashboard: 0 - off, 1 - on |
| 0x19 | Dashboard location: 0 - top, 1 - bottom |
| 0x22 | Show FPS: 0 - off, 1 - on |
| 0x2C | Picture Mode: 0 - standard, 1 - FPS, 2 - RTS/RPG, 3 - Movie, 4 - Reader, 5 - sRGB, 6-8 (?) - Custom modes |
| 0x2D | Source: 0 - HDMI1, 1 - HDMI2, 2 - DP, 3 - Type-C |
| 0x2E | Audio Input: 0 - from main, 1 - from PIP/PBP |
| 0x2F | OSD transparency: 0 - 0%, 1 - 20%, 2 - 40%, 3 - 60%, 4 - 80% |
| 0x30 | OSD display time: 0 - 5s, 1 - 10s, 2 - 15s, 3 - 20s, 4 - 25s, 5 - 30s |
| 0x32 | Quick Action Up: 0 - aim-stab, 1 - black eq, 2 - low-blue, 3 - volume, 4 - input, 5 - contrast, 6 - brightness, 7 - picture mode, 8 - kvm switch |
| 0x33 | Quick Action Down |
| 0x34 | Quick Action Right |
| 0x35 | Quick Action Left |
| 0x37 | Crosshair: 0 - off, 1-3 predefined, 4 - user-defined |
| 0x36 | Upload crosshair user-defined (yet to determine how) |
| 0x50 | Firmware version (read-only) |
| 0x69 | KVM device: 0 - USB-B, 1 - Type-C |
| 0x6B | KVM with USB-B: 0 - HDMI1, 1 - HDMI2, 2 - DP, 3 - Type-C |
| 0x6C | KVM with Type-C: 0 - HDMI1, 1 - HDMI2, 2 - DP, 3 - Type-C |
