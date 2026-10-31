# 01 - Hardware Teardown

 Opening up a generic Wi-Fi extender, identifying its main chips, and finding a working UART serial console.
 
---

## Device Summary
| Item | Detail | Notes | Datasheet |
| ------- | ----- | --------- | ------ |
| WiFi Extender | Trenzu WiFi Extender | Board: M-5357-B-V1.3 | N/A  |
| SoC | Broadcom BCM5357 | MIPS, 32-bit little-endian, 300 MHz | N/A |
| Flash | GigaDevice GD25Q64 | 64 Mbit (8 MB) SPI NOR | [GD25Q64C](https://www.tme.eu/Document/adfc3a1a269cb52cdae9532d711c82d9/gd25q64c.pdf) |
| RAM | Samsung K4H511638G | 512 Mbit (64 MB) DDR SDRAM | [K4H511638G](https://www.alldatasheet.com/html-pdf/351801/SAMSUNG/K4H511638G/297/1/K4H511638G.html) |

![board_labelled](/01%20Teardown/Photos/board_labelled.png)


## Teardown Process

1. **Opening the case:** Using plyers and hair dryer as heat gun was not available. 
2. **Photographing the board**  
3. **Identifying chips:** Read the markings on each large chip and matched them to datasheets.


## UART Access

Full analysis with all tests: [uart analysis](/01%20Teardown/uart_analysis.md)

**Summary:** The silkscreen labels on the UART header do not match the pins' real behavior. The pad labeled "RX" outputs the boot log, so it is the device's TX. The pad labeled "TX" produced no output, and I could not confirm that it accepts input. The console appears to be output only.

**Confirmed pinout**

| Silkscreen(as labelled) | Real function |
| ---- | ----- |
| GND | GND |
| "RX" | Device TX |
| "TX" | Device RX |
| "VCC" | VCC |

**Settings:** 115200 baud and ground reference taken from the power switch metal.


## Key Findings

- Board `M-5357-B-V1.3` uses a Broadcom BCM5357 (MIPS), a GD25Q64 8 MB SPI flash, and 64 MB of DDR RAM.
- The UART runs at 3.3 V and 115200 baud and outputs a boot log.
- Silkscreen labels on the UART pads do not match the real signal directions.
