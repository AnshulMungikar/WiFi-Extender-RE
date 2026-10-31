# 02 - Firmware Extraction

## Summary
How I tried to get the firmware off a generic Wi-Fi extender, first through UART and then by dumping the SPI flash chip directly.


## Equipment and Software

**Hardware**
- USB-to-serial (UART) adapter: [3.3V and 5V]

**Software**
- OS: fedora
- picocom: v2024-07


## Part 1: UART

**Goal:** Get a root console on the device.

### Wiring
The UART pads were connected to the USB-to-serial adapter following the pinout documented in [01 Teardown](/01%20Teardown/uart_analysis.md).

| Adapter | Device |
|---------|--------|
| GND | GND |
| RX | 'RX' |
| TX | 'TX' |

![Photo describing the UART wiring](/02%20Extraction/Photos/UART_wiring.jpg)

### Command
```bash
sudo picocom -b 115200 /dev/ttyUSB1
```
Settings: 115200 baud. 
Serial device: `/dev/ttyUSB1`.

### Result

After powering on the device, a boot log appeared in the terminal. The full log is saved in [uart_boot_log.txt](uart_boot_log.txt).

### Observations

- No root console or login prompt appeared after the boot log.
- The boot log ends after starting a program at 0x80001000.
- Pressing `Ctrl+c` during boot did nothing. This may mean the UART interface is receive-only from my side (the device's RX is not responding), as noted in [01 teardown](/01%20Teardown/uart_analysis.md).

### What went wrong

- **Problem:** UART gave output only, with no way to interact.
- **Likely cause:** Input from the adapter is not reaching the device, or console input is disabled in the firmware.
- **Next step:** Read the firmware directly from the flash chip.
