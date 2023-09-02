# Gigabyte M32U

This is truly awesome monitor that basically can be fully controlled
programmatically either over USB (HID device in KVM mode) or using DDC/CI (over HDMI/DP/Type-C).

The vendor codes are equal for HID and DDC/CI, as HID device effectively
encapsulates DDC/CI communication.

- This repository contains a fix for [ddcctl (OSX)](https://github.com/kfix/ddcctl)
  to allow control various aspects of the monitor - to be used on Intel MAC
- This repository contains a fix for [m1ddc (OSX)](https://github.com/waydabber/m1ddc)
  to allow control various aspects of the monitor - to be used on M1 MAC

The change can easily be adapted to [ddccontrol](https://github.com/ddccontrol/ddccontrol)
or [gbmonctl](https://github.com/kelvie/gbmonctl).

This likely applies to all Gigabyte monitors based on Realtek and using OSD Sidekick.

## Example

```bash
# Intel Mac
make -C ddcctl

# M1 Mac
make -C m1ddc
```

```bash
# Enable PIP
ddcctl/bin/release/ddcctl -d 1 -vendor_ext 0x0e0001
m1ddc/m1ddc display 1 set vendor_ext 0x0e0001

# Enable PBP
ddcctl/bin/release/ddcctl -d 1 -vendor_ext 0x0e0002
m1ddc/m1ddc display 1 set vendor_ext 0x0e0002

# Switch PBP/PIP inputs
ddcctl/bin/release/ddcctl -d 1 -vendor_ext 0x100001
m1ddc/m1ddc display 1 set vendor_ext 0x100001

# Disable PBP/PIP
ddcctl/bin/release/ddcctl -d 1 -vendor_ext 0x0e0000
m1ddc/m1ddc display 1 set vendor_ext 0x0e0000

# Switch KVM to USB-B
ddcctl/bin/release/ddcctl -d 1 -vendor_ext 0x690000
m1ddc/m1ddc display 1 set vendor_ext 0x690000

# Switch KVM to Type-C
ddcctl/bin/release/ddcctl -d 1 -vendor_ext 0x690001
m1ddc/m1ddc display 1 set vendor_ext 0x690001
```

## DDC codes

Standard DDC/CI codes supported.

| DDC code | Value |
|----|----|
| 0x10 | Brightness |
| 0x12 | Contrast |
| 0x62 | Volume |
| 0x87 | Sharpness |

## Vendor codes

ddcctl/bin/release/ddcctl -d 1 -vendor_ext 0xXXYYZZ
m1ddc/m1ddc display 1 set vendor_ext 0xXXYYZZ

| XX   | Description | YY | ZZ |
|------|-------------|----|----|
| 0x02 | Black Equalizer | 0x0 | 0x0-0xA (0-10) |
| 0x03 | Color Temperature | 0x0 | 0 - cool, 1 - normal, 2 - warm, 3 - user-defined |
| 0x04 | Color Temperature Red | 0x0 | 0x0-0x64 (0-100) |
| 0x05 | Color Temperature Blue | 0x0 | 0x0-0x64 (0-100) |
| 0x06 | Color Temperature Green | 0x0 | 0x0-0x64 (0-100) |
| 0x07 | Gamma | 0x0 | 0 - off, 1 - 1.8, 2 - 2.0, 3 - 2.2, 4 - 2.4, 5 - 2.6 |
| 0x08 | Color Vibrance | 0x0 | 0x0-0x14 (0-20) |
| 0x09 | Overdrive | 0x0 | 0 - quality, 1 - balance, 2 - speed |
| 0x0A | Aim Stabilizer | 0x0 | 0 - off, 1 - on |
| 0x0B | Low Blue Light | 0x0 | 0x0-0xA (0-10) |
| 0x0C | Free Sync | 0x0 | 0 - off, 1 - on |
| 0x0D | Super Resolution | 0x0 | 0-4 |
| 0x0E | PBP/PIP Mode | 0x0 | 0 - off, 1 - PIP, 2 - PBP |
| 0x0F | PBP/PIP Source | 0x0 | 0 - HDMI1, 1 - HDMI2, 2 - DP, 3 - Type-C |
| 0x10 | PBP/PIP Switch | 0x0 | use 1 |
| 0x13 | PBP/PIP Audio Switch | 0x0 | use 1 |
| 0x14 | PIP Size | 0x0 | 0 - large, 1 - medium, 2 - small |
| 0x15 | PIP Location | 0x0 | 0 - top-left, 1 - top-right, 2 - bottom-left, 3 - bottom-right |
| 0x18 | Dashboard | 0x0 | 0 - off, 1 - on |
| 0x19 | Dashboard location | 0x0 | 0 - top, 1 - bottom |
| 0x1A | Set CPU Temperature | 0x0 | Use: `-vendor_ext 0x1A00ZZWW00` |
| 0x1B | Set CPU Frequency | 0x0 | Use: `-vendor_ext 0x1B00ZZWW00` |
| 0x1C | Set CPU FAN | 0x0 | Use: `-vendor_ext 0x1C00ZZWW00` |
| 0x1D | Set CPU Usage | 0x0 | Use: `-vendor_ext 0x1D00ZZWW00` |
| 0x1E | Set GPU Temperature | 0x0 | Use: `-vendor_ext 0x1E00ZZWW00` |
| 0x1F | Set GPU Frequency | 0x0 | Use: `-vendor_ext 0x1F00ZZWW00` |
| 0x20 | Set GPU FAN | 0x0 | Use: `-vendor_ext 0x2000ZZWW00` |
| 0x21 | Set GPU Usage | 0x0 || Use: `-vendor_ext 0x2100ZZWW00` |
| 0x22 | Show FPS | 0x0 | 0 - off, 1 - on |
| 0x23 | Game Timer Mode | 0x0 | 0 - off, 1 - up, 2 - down |
| 0x25 | Get Game Current Timer (read-only) | ? | ? |
| 0x26 | Game Timer Set | minutes | seconds |
| 0x27 | Game Timer | 0x0 | 0 - pause, 1 - resume |
| 0x28 | Game Counter | 0x0 | 0 - off, 1 - on |
| 0x29 | Get Game Current Counter (read-only) | ? | ? |
| 0x2A | Game Counter Set | 0x0 | 0x0-0x63 (0-99) |
| 0x2B | Game Timer/Counter/FPS Location | 0 - left, 1 - right | 0 - top, 1 - center, 2 - bottom |
| 0x2C | Picture Mode | 0x0 | 0 - standard, 1 - FPS, 2 - RTS/RPG, 3 - Movie, 4 - Reader, 5 - sRGB, 6-8 (?) - Custom modes |
| 0x2D | Source | 0x0 | 0 - HDMI1, 1 - HDMI2, 2 - DP, 3 - Type-C |
| 0x2E | Audio Input | 0x0 | 0 - from main, 1 - from PIP/PBP, 2 - auto |
| 0x2F | OSD transparency | 0x0 | 0 - 0%, 1 - 20%, 2 - 40%, 3 - 60%, 4 - 80% |
| 0x30 | OSD display time | 0x0 | 0 - 5s, 1 - 10s, 2 - 15s, 3 - 20s, 4 - 25s, 5 - 30s |
| 0x31 | LED Indicator | 0x0 | 0 - always on, 1 - always off, 2 - standby on |
| 0x32 | Quick Action Up | 0x0 | 0 - aim-stab, 1 - black eq, 2 - low-blue, 3 - volume, 4 - input, 5 - contrast, 6 - brightness, 7 - picture mode, 8 - kvm switch |
| 0x33 | Quick Action Down | 0x0 | as Quick Action Up |
| 0x34 | Quick Action Right | 0x0 | as Quick Action Up  |
| 0x35 | Quick Action Left | 0x0 | as Quick Action Up  |
| 0x37 | Crosshair | 0x0 | 0 - off, 1-3 predefined, 4 - user-defined |
| 0x36 | Upload crosshair user-defined | ? | ? |
| 0x38 | Get Firmware version (read-only) | ? | ? |
| 0x4A | Set Mouse DPI | 00 | Use: `-vendor_ext 0x4A00ZZWW00` |
| 0x50 | Get Firmware version (read-only) | ? | ? |
| 0x53 | Get HDR (read-only) | ? | ? |
| 0x55 | N/A Mouse DPI | ? | ? |
| 0x56 | N/A CPU Temperature | ? | ? |
| 0x57 | N/A CPU Frequency | ? | ? |
| 0x58 | N/A CPU FAN | ? | ? |
| 0x59 | N/A CPU Usage | ? | ? |
| 0x5A | N/A GPU Temperature | ? | ? |
| 0x5B | N/A GPU Frequency | ? | ? |
| 0x5C | N/A GPU FAN | ? | ? |
| 0x5D | N/A GPU Usage | ? | ? |
| 0x69 | KVM switch device | 0x0 | set 1 |
| 0x6A | KVM switch button | 0x0 | 0 - disabled, 1 - enabled |
| 0x6B | KVM with USB-B | 0x0 | 0 - HDMI1, 1 - HDMI2, 2 - DP, 3 - Type-C |
| 0x6C | KVM with Type-C | 0x0 | 0 - HDMI1, 1 - HDMI2, 2 - DP, 3 - Type-C |
