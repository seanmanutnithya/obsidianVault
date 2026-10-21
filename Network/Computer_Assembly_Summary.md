---
title: Computer Assembly (Hardware / Software Installation)
tags: [computer-assembly, hardware, bios, uefi, course-notes]
source: Course_Computer_Assembly_Hardware_Software_Installation_2.pdf
course: Institute of Technology of Cambodia (ITC)
created: 2026-10-21
---

# Computer Assembly (Hardware / Software Installation)

## Overview

This course covers three main parts:

1. Introduction to computer assembly
2. Computer hardware installation
3. BIOS setup and bootable OS

Computer assembly means putting together all the hardware components of a computer to build a complete working system. Work is done in a fixed order: physical installation first, then power and cables, then BIOS setup, and finally the operating system.

## I. Introduction to Computer Assembly

**Characteristics**

- Combine hardware components into one system
- Ensure all parts are properly connected
- Prepare the computer for software installation
- Enable the computer to function correctly

**Examples**

- Installing CPU, RAM, and motherboard
- Connecting power supply and storage devices
- Assembling a desktop computer system

## II. Computer Hardware Installation

Common components to install: case, CPU and thermal paste, CPU fan/cooler, storage (SSD and HDD), network or sound card, RAM and GPU, motherboard, power supply (PSU), case fans.

### Workspace preparation

- Good ventilation and adequate lighting
- Comfortable room temperature
- Workbench accessible from all sides
- Anti-static mat on the workbench
- Small container for screws and small parts

### Suggested assembly order

Use this order from the slides as a checklist:

1. **Open the case:** Shutdown, disconnect cables, remove screws, slide or remove the side panel.
2. **Install the PSU:** Check wattage and case compatibility, align screw holes, insert and tighten screws.
3. **Prepare the motherboard:** Place it on an anti-static surface. Attach the CPU, RAM and M.2 SSD while it is outside the case.
4. **Install the CPU:** Check the socket and locking mechanism, handle by the edges, follow the socket type.
5. **Apply thermal paste:** Use a small amount in the center of the CPU. Do not use too much, and do not touch the surfaces with your fingers.
6. **Install the heat sink/fan:** Connect to the CPU_FAN header.
7. **Install RAM:** Install before the motherboard goes into the case. Align the notch with the key.
8. **Install the M.2 SSD:** Insert at an angle, press down gently, and secure with the screw. Do not force it.
9. **Mount the motherboard in the case:** Install the standoffs that line up with the holes, align the I/O panel, then insert and tighten all screws.
10. **Install storage (SATA HDD/SSD):** Mount in a bay, then connect the SATA data cable and SATA power cable.
11. **Install the GPU:** Use the PCIe x16 slot, remove the expansion-slot cover, and connect PCIe power if needed.
12. **Install NIC and sound adapter:** Use the correct PCI or PCIe slot, press down until seated, and secure the bracket.
13. **Connect internal cables:** Power cables, data cables, and front-panel buttons and LEDs.
14. **Connect motherboard power:** 24-pin ATX and CPU power (EPS12V).
15. **Connect external cables:** Monitor, keyboard, mouse, Ethernet, and power.
16. **Set up the monitor and UPS.**

### Power supply cable connections

| Connector | Connects to |
|---|---|
| 24-pin ATX | Motherboard |
| 4/8-pin EPS12V | CPU power |
| 6/8-pin PCIe | Dedicated GPU |
| SATA power | SATA HDD/SSD and other SATA devices |

Route cables neatly so they do not block airflow.

### RAM configurations

- **1 module:** Use the motherboard's recommended DIMM slot.
- **2 modules:** Use the paired slots for dual-channel mode. On a typical 4-slot board this is often DIMM_A2 + DIMM_B2.
- **4 modules:** Fill all DIMM slots and enable dual-channel.

### Monitor connection

- **Integrated graphics:** Connect the HDMI or DisplayPort cable to the motherboard's video output.
- **Dedicated GPU:** Connect the cable to the GPU's port, not the motherboard. The GPU must be used for display output.

Display settings: Windows Settings → System → Display. For several monitors, use Identify Displays and then Arrange Displays.

Display modes: Duplicate, Extend, Show only on 1, Show only on 2.

### Key warnings

- Never force a connector or cable.
- Plug in the power cable **after** all other cables are connected.
- Do not force an M.2 SSD into its slot.
- Handle all components by their edges.
- Install only the standoffs that line up with the motherboard holes.

### UPS installation

Power-on order: Place UPS → Connect UPS to mains → Connect computer and monitor to UPS → Turn on UPS → Turn on computer.

## III. BIOS Setup and Bootable OS

### POST (Power-On Self-Test)

- The BIOS is firmware stored in a non-volatile chip on the motherboard.
- At boot, the BIOS runs POST to check the CPU, RAM, storage, and USB devices.
- If an error is found, the computer shows an error message or beep code.
- Press a special key (such as F2, Del, or F10) during boot to enter BIOS Setup.

### BIOS Setup and CMOS

- BIOS Setup configures hardware settings.
- Settings are saved in CMOS memory, which the motherboard battery powers.
- If the CMOS battery dies, all BIOS settings are lost. Replace the battery and reconfigure the settings.

### BIOS vs UEFI

| Feature | Traditional BIOS | UEFI |
|---|---|---|
| Interface | Text-based | Graphical |
| Boot method | MBR | GPT (with EFI System Partition) |
| Max disk size | Typically up to 2 TB | Supports very large disks (over 2 TB) |
| Boot speed | Slower | Faster |
| Secure Boot | Not supported | Supported |

UEFI is the modern replacement for BIOS. Both start the computer and prepare it to load an operating system.

### Boot device setup

- **Boot device:** Any device that can contain bootable software.
- **Boot order (boot priority):** The sequence in which firmware checks devices. The first bootable device found is used.

| Boot device | Example | Typical use |
|---|---|---|
| NVMe SSD | Internal M.2 SSD | Normal OS boot |
| SATA SSD/HDD | 2.5" SSD or HDD | OS or data storage |
| USB flash drive | Bootable Windows or Linux USB | OS installation |
| DVD/CD | Installation DVD | Legacy OS installation |

### How a computer boots (power on to desktop)

1. **Power on:** Press the power button. The PSU supplies power to the components.
2. **Firmware starts:** The CPU runs code from the BIOS/UEFI chip and initializes hardware.
3. **POST:** Checks essential hardware such as CPU, RAM, and storage.
4. **Load BIOS/UEFI settings:** Reads saved settings (date and time, boot order, hardware configuration).
5. **Select boot device:** Checks boot devices in boot order.
6. **Load bootloader:** Loads the bootloader from the selected device (for example, Windows Boot Manager or GRUB).
7. **Operating system loads:** The bootloader starts the OS and loads the kernel into memory.
8. **System initialization:** The OS loads drivers, services, and settings, and detects hardware.
9. **Login and desktop:** The login screen appears, and the desktop is ready after authentication.

Short version: Power On → Firmware → POST → Load Settings → Select Boot Device → Bootloader → Operating System → Ready to Use

## Key Terms

- **POST:** Power-On Self-Test. The startup hardware check.
- **BIOS:** Basic Input/Output System. Legacy firmware interface.
- **UEFI:** Unified Extensible Firmware Interface. Modern replacement for BIOS.
- **CMOS:** Memory chip that stores BIOS settings, powered by a battery.
- **Bootloader:** Program that starts the operating system (for example, GRUB).
- **Boot priority:** Order in which devices are checked for a bootable OS.
- **Standoffs:** Spacers that lift the motherboard off the case.
- **Dual-channel:** Memory mode that uses paired RAM slots for better bandwidth.
- **PSU:** Power supply unit.
- **EPS12V:** CPU power connector.
- **TIM:** Thermal Interface Material (thermal paste).

## Review Questions

1. What are the four characteristics of computer assembly?
2. Why should RAM be installed before the motherboard is placed in the case?
3. Which PSU connector powers the motherboard, and which powers the CPU?
4. What is the recommended RAM configuration for two modules, and why?
5. Which port should a monitor connect to when a dedicated GPU is installed?
6. Why should the power cable be plugged in last?
7. What happens if the CMOS battery dies?
8. What is the difference between BIOS and UEFI?
9. Put these steps in order: Bootloader, POST, Power on, Select boot device, Operating system loads.
10. Why does the boot order matter?

---

*Remember: Practice makes perfect.*
