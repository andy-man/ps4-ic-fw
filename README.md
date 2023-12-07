# About

This collection was kindly provided by zecoxao

**Structure:** [eap/emc/torus] / [type] / [fw_range]_[md5].2bls

**Example:** `emc/24/1000-1001_421ea7fec14cf827f6380326ab9fe42b.2bls`

# EMC and EAP

PS4 southbridge contains two processors named EMC and EAP used on boot, during rest mode and for servicing.

The two processors are on the same chip. It is a SoC (System on Chip).

More info can be found [here](https://www.psdevwiki.com/ps4/Southbridge)

## EMC IPL (Initial Program Loader)

EMC could stand for External Micro Controller. EMC was named MediaCon by some people when its name was still unknown.

The role of EMC is to load EMC IPL, to be an interface for icc for the main APU kernel and Syscon and to offer a debug interface via UART that does not rely on Syscon or main APU. EMC runs its own FreeBSD kernel. 

It is a Marvell Armada, an ARM-based SoC. Sony stuck a PCIe bridge on it. It exposes ARM peripherals to the x86 side. There is some extra stuff (e.g. HPET, ACPI stuff).

EMC cpuid = **412FC231** (ARM Cortex-M3 r2p1). CPU clock: maybe about **100MHz**.

## EAP KBL (Kernel Boot Loader)

EAP could stand for External Application Processor.

The role of EAP is to handle media (online Wireless/GbLAN, Bluray Drive and HDD/SSD) even when the PS4 is in standby mode. EAP runs its own FreeBSD kernel in standby mode, activated to handle tasks such as downloading games updates while the PS4 is in standby.

It handles several tasks to offload the APU:

* Network connections: Wireless and GbLAN, including background downloading and PlayGo
* File handling (Bluray Drive, Harddrive and USB 3.0), including background caching
* Main serial flash handling

EAP consists of Marvell PJ4C B0 rev 1 cores, ARMv7 CORTEX-A8 running FreeBSD 9 kernel. CPU clock: **500MHz**. DDR clock: **800MHz**.

As EAP Core software is unsigned, unencrypted and easily replaceable on PS4 HDD with a PS4 kernel exploit, it is possible to run homebrew code on EAP processor.

# Syscon

Syscon is, together with Southbridge, one of the main chips responsible for taking care of the functioning of APU, peripherals, etc.

PS4 Syscon is codenamed Colwick. It is a custom Renesas RL78/G13.

Folder contains all FW found for now.

[More info](https://www.psdevwiki.com/ps4/Syscon_Hardware)

# Torus (WiFi and Bluetooth)

The Wireless communication module firmware is stored within the Flash-Main of the PS4 in a file designated C0020001. It is updated during the firmware updates of the PS4. 

This firmware is known to get corrupt, rendering the Wi-Fi and Bluetooth broken. This means that the DualShock controller cannot function in the XMB. However, the controller can still be used in safe mode as this is the only software of the PS4 that does not utilize the Wireless communication module firmware at all, rather it only connects to the controller via USB. 

This problem is repairable, given you have a copy of the same firmware for your module.

## How to know if the PS4 torus firmware is corrupted?

* If DS4 controller does not sync anywhere but the safe mode menu then the Bt/Wifi firmware is corrupted.

* If DS4 controller does not sync in safe mode, it may be issue on southbridge/usb port.

* If Bt/Wifi firmware is VALID but there is still no controller sync anywhere other than safemode, the PS4 may physically need a new module which match with its revision.
