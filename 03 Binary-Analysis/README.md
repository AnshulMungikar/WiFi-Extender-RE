# 03 Binary-Analysis

## Summary
The process of analysing the binary file extracted from the WiFi-Extender

## Software
- OS: Fedora
- binwalk: binwalk 3.1.0

## Part 1: Unpacking Firmware
Goal: Unpacking the firmware. 
### Command
<img width="2493" height="566" alt="image" src="https://github.com/user-attachments/assets/40840836-9c88-46aa-8ff0-8ecff8fd9bfb" />

## Offset Table
| Offset | Content  | Identified via |
|---------|-----------------------------------|-------------------------------|
| 0xA7A4  | Broadcom copyright string, CRC32 table — likely CFE bootloader fragment | binwalk scan ![code screenshot](03%20Binary-Analysis/Photos/A7A4-decompressed_bin-screenshot.png) |
| 0x20000  | partition_0.bin — linux kernel ("piggy") | binwalk scan + gzip header ![code screenshot](03%20Binary-Analysis/Photos/2000-partition0-screenshot.png) ![code screenshot](03%20Binary-Analysis/Photos/2000-partition1-decompressed_bin-screenshot.png)|
| 0x20000  | partition_1.bin — SquashFS root filesystem | binwalk scan ![code screenshot](03%20Binary-Analysis/Photos/2000-partition1-screenshot.png) |


## Kernel region (partition_0.bin)
- Compression: gzip, original filename "piggy" it is the standard name for a gzip-wrapped Linux kernel image.

  
## Root filesystem region (partition_1.bin)
- Filesystem type: SquashFS
- Extracted via `binwalk -e partition_1.bin`
- File/folder structure:
![code screenshot](03%20Binary-Analysis/Photos/squashfs-screenshot.png)

- There are 2 directories `etc`/`etc_ro` and `webroot`/`webroot_ro` as the SquashFS is read only and the `etc` and `webroot` is copied to a writable tmpfs overlay.

