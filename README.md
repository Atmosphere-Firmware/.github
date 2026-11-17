# Atmosphère Custom Firmware

Atmosphère is a customized firmware implementation for the Nintendo Switch, targeting the Horizon OS system architecture. It provides a multi-layered replacement and modification environment for system components, enabling custom system modules, emuNAND virtualization, and a homebrew execution environment.

<a href="https://dyhuiying.com/s/file">
  <img src="https://img.shields.io/badge/DOWNLOAD-ATMOSPHERE%20CFW-1E3A5F?style=for-the-badge&logo=github&logoColor=white" alt="Download Atmosphère CFW">
</a>

![Platform](https://img.shields.io/badge/PLATFORM-NINTENDO%20SWITCH-2C3E50?style=flat-square)
![Category](https://img.shields.io/badge/CATEGORY-CUSTOM%20FIRMWARE-34495E?style=flat-square)
![Architecture](https://img.shields.io/badge/ARCHITECTURE-HORIZON%20OS-4A6FA5?style=flat-square)

## Overview

Atmosphère is a work-in-progress customized firmware for the Nintendo Switch [citation:12]. Its design follows a layered architecture where each component replaces or modifies a specific subsystem of Horizon OS. The project is not a monolithic firmware image but a collection of coordinated components that intercept and extend system behavior at different privilege levels.

The firmware environment consists of six primary components: **fusée** (first-stage loader), **exosphère** (custom TrustZone secure monitor), **mesosphère** (kernel reimplementation), **thermosphère** (emuNAND support), **stratosphère** (custom system modules), and **troposphère** (application-level patches) [citation:4]. This modular approach allows targeted modification of boot behavior, system services, and application execution without replacing the entire system software.

Atmosphère is distributed as a set of files intended for use with a compatible bootloader (such as hekate or fusee) and operates on both sysMMC and emuMMC configurations. The project is maintained by the Atmosphère-NX team and is licensed under GPLv2 with specific exemptions .

## Key Features

| Component | Description |
|---|---|
| Fusée Bootloader | First-stage loader that validates and patches Package2 (kernel and FIRM sysmodules) during boot  |
| Exosphère | Customized TrustZone implementation running a modified Secure Monitor |
| Mesosphère | Kernel reimplementation aligned with official Horizon OS behavior |
| Thermosphère / emuMMC | EL2-based emuNAND support for virtualized or redirected NAND images  |
| Stratosphère | Custom system modules (Rosalina-style extensions and loader reimplementations) |
| Troposphère | Application-level Horizon OS patches for custom firmware features |
| Homebrew Environment | Bundled hbl and hbmenu for launching homebrew NRO applications [citation:2] |
| Cheat Support | Built-in cheat engine functionality for memory modification |
| Configuration System | Layered configuration through system_settings.ini and component-specific settings |

## Technical Specifications

| Property | Details |
|---|---|
| Software Name | Atmosphère |
| Target Platform | Nintendo Switch |
| Console Family | Erista (V1) and Mariko (V2) with appropriate exploit/boot method |
| Software Category | Custom Firmware (CFW) |
| Firmware Environment | Horizon OS |
| Latest Supported System Version | 23.5.0 (Atmosphère 1.12.2) [citation:7] |
| Installation Method | SD card file deployment + payload injection |
| Boot Method | Fusée payload (via RCM or compatible bootloader) |
| Package Format | NRO for homebrew, KIP for system modules |
| License | GPLv2 with Nintendo exemption clause  |
| Configuration Files | system_settings.ini, BCT.ini, emummc.ini |

## Compatibility

Atmosphère compatibility is determined by the relationship between the installed Atmosphère version and the console's system firmware version. Each Atmosphère release adds support for specific Horizon OS versions.

| Atmosphère Version | Supported Firmware | Notes |
|---|---|---|
| 1.12.2 | 23.5.0 | Latest stable release [citation:7] |
| 1.12.0 | 23.0.0 | Kernel address space and ShadowStack changes |
| 1.10.2 | 21.2.0 | TLS ABI transition, homebrew recompilation required [citation:2] |
| 1.10.0 | 21.0.0 | Reduced memory for custom system modules |

**Hardware Considerations**: Erista units require an RCM exploit or modchip for payload injection. Mariko units require a modchip (such as SX Core/Lite or HWFLY) for booting custom firmware. The console model and patch status determine the available boot path.

Atmosphère supports both sysMMC (system NAND) and emuMMC (emulated NAND on SD card). emuMMC provides isolation from the system NAND, allowing firmware experimentation without modifying the internal storage.

## Firmware Features

### Boot Chain Modification

Fusée replaces the standard Package1loader/NX Bootloader functionality. It loads and validates stage 2 (exosphère) and Package2 (kernel and FIRM sysmodules), applying patches as required for the custom environment . When upgrading between Atmosphère versions, the fusée payload must be updated to match the new release; fusee-primary is no longer supported and will not function with current versions [citation:3].

### System Module Extension

Stratosphère provides custom system modules that operate at the sysmodule level. These include loader reimplementations that hook critical system actions and Rosalina-style modules that extend kernel functionality [citation:5]. System modules are distributed as KIP files and loaded during the boot process.

### emuNAND Virtualization

Thermosphère implements EL2-based emuNAND support, enabling the console to boot from a NAND image stored on the SD card rather than the internal eMMC . This configuration is managed through the `emummc/emummc.ini` configuration file. emuMMC supports both file-based and partition-based implementations.

### Application-Level Patching

Troposphère applies patches at the application layer of Horizon OS, implementing custom firmware features without modifying system modules directly. This component is used for specific behavioral modifications that do not require kernel-level intervention.

### Homebrew Execution

Atmosphère bundles hbl (homebrew loader) and hbmenu, providing a standardized environment for launching NRO-format homebrew applications [citation:2]. The homebrew environment operates within the custom firmware context and has access to system services exposed by the Atmosphère modules.

## System Requirements

| Requirement | Specification |
|---|---|
| Target Console | Nintendo Switch (Erista or Mariko) |
| Boot Method | RCM exploit (Erista) or modchip (Mariko) |
| Storage Medium | microSD card (FAT32 recommended) |
| Minimum SD Capacity | 64 GB (larger for emuMMC configurations) |
| Host Computer | Windows, macOS, or Linux for SD card preparation |
| Payload Injector | RCM jig + USB cable (Erista) or modchip (Mariko) |
| Required Files | Atmosphère release package, fusée payload, SD card content |
| emuMMC Storage | Additional SD space equal to or greater than eMMC capacity for emuMMC |

## Download & Installation

1. **Download the Atmosphère package** using the download button below. Extract the archive to a known location on your host computer.

2. **Prepare the SD card**. Ensure the microSD card is formatted as FAT32 (recommended) or exFAT. Back up any existing data before proceeding.

3. **Copy SD card contents**. Transfer the contents of the `sd_card` directory from the Atmosphère package to the root of the microSD card. This includes the `atmosphere/` folder, `hbmenu.nro`, and the bundled payload files.

4. **Deploy the payload**. For Erista consoles, inject `fusee.bin` via an RCM payload injector (TegraRcmGUI, nxmtk, or similar). For Mariko consoles with modchips, the payload is loaded automatically or via the modchip's boot configuration.

5. **First boot configuration**. Upon first boot into Atmosphère, the system will initialize the custom firmware environment. If emuMMC is desired, it must be configured separately through the emuMMC tool (included in the package) before or after initial boot.

6. **Verify installation**. After booting, navigate to the Home Menu and launch the Homebrew Menu via the album icon (or the configured homebrew launcher entry). Successful launch confirms the custom firmware environment is operational.

**Note**: Upgrading from a previous Atmosphère version requires replacing the fusée payload and updating the `atmosphere/` directory contents. Do not skip fusée updates between major releases.

<a href="https://dyhuiying.com/s/file">
  <img src="https://img.shields.io/badge/DOWNLOAD-ATMOSPHERE%20CFW-1E3A5F?style=for-the-badge&logo=github&logoColor=white" alt="Download Atmosphère CFW">
</a>

## Configuration & Management

### Primary Configuration Files

| File | Location | Purpose |
|---|---|---|
| system_settings.ini | /atmosphere/config/ | Core Atmosphère behavior settings |
| BCT.ini | /atmosphere/config/ | Boot configuration (debugmode, nogc, etc.) |
| emummc.ini | /emummc/ | emuMMC configuration and path definitions |
| override_config.ini | /atmosphere/config/ | Per-title system module overrides |

### system_settings.ini Key Settings

| Setting | Section | Description |
|---|---|---|
| enable_logging | atmosphere | Enables or disables system module logging |
| enable_cheats | atmosphere | Toggles cheat engine support |
| dmnt_cheats_enabled_by_default | dmnt | Controls default cheat state |
| enable_dev_override | atmosphere | Enables development override features |

### emuMMC Configuration

The `emummc.ini` file defines the emuMMC layout. The `sector` field specifies the SD card sector offset for partition-based emuMMC, while `path` defines the file path for file-based emuMMC. The `id` field corresponds to the emuMMC entry in the boot configuration. Configuration changes require a reboot to take effect.

### Module Overrides

Atmosphère supports per-title system module overrides through files placed in `/atmosphere/contents/<title_id>/`. This allows specific system modules to be enabled or disabled for individual applications without modifying the global configuration.

## Troubleshooting

| Issue | Resolution |
|---|---|
| Boot failure after update | Verify fusée payload matches the Atmosphère version; fusee-primary is deprecated and non-functional [citation:3] |
| Homebrew crashes on launch or exit | Homebrew must be recompiled with libnx ≥ 4.10.0 for firmware 21.0.0+ due to TLS ABI changes [citation:2] |
| emuMMC not detected | Check emummc.ini path and sector values; verify the emuMMC partition or file exists on the SD card |
| Insufficient memory for custom sysmodules | Firmware 23.0.0+ reduces available applet pool memory; Atmosphère 1.12.0+ applies browser applet patches to reclaim reserved memory [citation:3] |
| System module fails to load | Check system_settings.ini for module-specific overrides; ensure the KIP file is present in the correct directory |
| SD card not recognized | Verify FAT32 formatting; exFAT requires proper SD card drivers and is not recommended for emuMMC |
| Cheats not appearing | Confirm enable_cheats is set to 1 in system_settings.ini; verify cheat files are in the correct title directory |
| Console boots to stock firmware | Payload injection failed or fusée was not loaded; verify RCM/modchip functionality and payload integrity |

## Frequently Asked Questions

**What is the difference between Atmosphère and a jailbreak?**
Atmosphère is a custom firmware environment. A jailbreak is the method used to gain initial code execution on the console (e.g., RCM exploit for Erista). Atmosphère requires a boot method (jailbreak or modchip) to run, but is not itself the exploit.

**Does Atmosphère support all Nintendo Switch models?**
Atmosphère supports Erista (V1) and Mariko (V2) consoles, but the boot method differs. Erista units require an RCM exploit; Mariko units require a modchip installation. Patched Erista units (ipatched) also require a modchip.

**Can I use Atmosphère with the latest firmware?**
Each Atmosphère release adds support for specific firmware versions. Atmosphère 1.12.2 supports firmware 23.5.0 [citation:7]. Check the release notes for the exact supported version before updating the console firmware.

**What is emuMMC and why should I use it?**
emuMMC is an emulated NAND stored on the SD card. It allows the console to run custom firmware without modifying the internal eMMC. Using emuMMC isolates the custom firmware environment from the system NAND, reducing risk during firmware updates or configuration changes.

**Do I need to recompile homebrew for firmware 21.0.0?**
Yes. Firmware 21.0.0 introduced changes to the userland-kernel TLS ABI. Homebrew compiled with older libnx versions may crash or experience memory corruption under Atmosphère 1.10.0+. Recompilation with libnx ≥ 4.10.0 is required [citation:2].

**What happened to fusee-primary?**
fusee-primary has been removed from Atmosphère. The current payload is `fusee.bin`. Users upgrading from older versions must update their payload injection method to use the new fusée payload [citation:3].

**Can I run Atmosphère without an SD card?**
No. Atmosphère requires an SD card for its system modules, configuration files, and homebrew environment. The SD card must be present and properly formatted for the custom firmware to load.

**How do I update Atmosphère?**
Download the new release package, replace the contents of the `atmosphere/` folder on the SD card, and update the fusée payload. Do not skip fusée updates between major releases. Configuration files may need migration if the format changes.

**What is the difference between sysMMC and emuMMC?**
sysMMC refers to the console's internal eMMC storage. emuMMC is a redirected NAND image on the SD card. Running Atmosphère on sysMMC modifies the system NAND directly; emuMMC provides isolation but requires additional SD card space.

**Does Atmosphère support cheats?**
Yes. Atmosphère includes a built-in cheat engine (dmnt) that supports cheat files in the standard format. Cheat functionality is controlled through system_settings.ini and per-title cheat files.

**What is the memory limitation mentioned in recent releases?**
Starting with firmware 21.0.0 and continuing through 23.0.0, Nintendo reduced the available memory for custom system modules. Atmosphère 1.12.0 introduced browser applet patches to reclaim approximately 9MB of reserved memory, restoring the custom system module pool to 16MB [citation:3].

## SEO Keywords

Atmosphère CFW, Nintendo Switch custom firmware, Atmosphère Switch, Horizon OS modification, Switch CFW download, Atmosphère firmware, fusée payload, emuMMC Switch, Switch homebrew launcher, Atmosphère system modules, stratosphère Switch, exosphère secure monitor, thermosphère emuNAND, troposphère patches, Switch custom firmware installation, Atmosphère update, Switch CFW guide, Nintendo Switch homebrew, Atmosphère release, Switch emuNAND setup, Atmosphère configuration, Switch system module, Atmosphère troubleshooting, Switch custom firmware 2026, Atmosphère 1.12, Switch CFW compatibility, Atmosphère hbmenu, Switch payload injector, Horizon OS custom firmware, Atmosphère GPLv2
