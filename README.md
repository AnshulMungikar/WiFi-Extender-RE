# WiFi-Extender-RE
Firmware extraction and reverse engineering of a WiFi extender.

## Motivation & Background
I had an old, unused WiFi extender lying around my house. Driven by curiosity, I wanted to answer a few questions:
- What does the firmware actually consist of?
- Can I find any security vulnerabilities or misconfigurations in the device?

**Status** : In progress (teardown complete)

## Target Device

<img width="2258" height="1750" alt="board_labelled" src="https://github.com/user-attachments/assets/e2a93fbc-82e8-4c54-807c-f0c306ce0443" />

### Device Summary Table
| Item | Detail | Notes | Datasheet |
|------|--------|-------|-----------|
| WiFi Extender | Trenzu WiFi Extender | Board: M-5357-B-V1.3 | N/A |
| SoC | Broadcom BCM5357 | MIPS, 32-bit little-endian, 300 MHz | N/A |
| Flash | GigaDevice GD25Q64 | 64 Mbit (8 MB) SPI NOR | [GD25Q64C](https://www.tme.eu/Document/adfc3a1a269cb52cdae9532d711c82d9/gd25q64c.pdf) |
| RAM | Samsung K4H511638G | 512 Mbit (64 MB) DDR SDRAM | [K4H511638G](https://www.alldatasheet.com/html-pdf/351801/SAMSUNG/K4H511638G/297/1/K4H511638G.html) |


