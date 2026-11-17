
<h1 align="center">Atmosphère Custom Firmware</h1>

<p align="center">
  <strong>Firmware Architecture. System Modification. Homebrew Environment.</strong>
</p>

<p align="center">
  Nintendo Switch Custom Firmware · Horizon OS · System-Level Development
</p>

<p align="center">
  <img src="https://img.shields.io/badge/platform-Nintendo%20Switch-D94B4B?style=flat-square">
  <img src="https://img.shields.io/badge/category-Custom%20Firmware-D94B4B?style=flat-square">
  <img src="https://img.shields.io/badge/license-GPL--2.0-555555?style=flat-square">
  <img src="https://img.shields.io/badge/release-1.12.1-333333?style=flat-square">
</p>

## Overview

Atmosphère is a customized firmware project for the Nintendo Switch, designed around a modular reimplementation of multiple system components.

The project modifies and extends different layers of the console's software environment, including the boot process, TrustZone, kernel, system modules, and application-level system behavior.

Rather than functioning as a single firmware modification, Atmosphère uses a layered architecture in which individual components are responsible for specific system functions.

Its architecture provides a foundation for custom system behavior, homebrew integration, configuration management, and additional firmware-level functionality.

## Technical Architecture

Atmosphère is organized into six primary components.

| Component | Description | Technical Role |
|---|---|---|
| Fusée | First-stage custom loader | Boot process and firmware loading |
| Exosphère | Customized TrustZone implementation | Secure monitor functionality |
| Thermosphère | EL2-based EmuNAND support | Virtualized and redirected NAND |
| Mesosphère | Custom kernel implementation | Horizon OS kernel functionality |
| Stratosphère | Custom system modules | System services and kernel extensions |
| Troposphère | Application-level system patches | Horizon OS customization |

### Secondary Components

**EmuMMC**

Provides support for backing up and using virtualized or redirected NAND images.

**Libraries**

Contains supporting software components used throughout the firmware architecture.

## Core Components

| Component | Description | Technical Role |
|---|---|---|
| Fusée | Firmware boot loader | Boot initialization |
| Exosphère | TrustZone customization | Secure monitor |
| Mesosphère | Kernel reimplementation | Kernel operations |
| Thermosphère | EmuNAND functionality | NAND virtualization |
| Stratosphère | System module framework | System-level extensions |
| Troposphère | Application-level patches | OS behavior modification |
| EmuMMC | Redirected NAND environment | Storage separation |
| Configuration | Firmware configuration files | Runtime configuration |

## Key Features

### Firmware Architecture

- Modular system design with independent firmware components.
- Customized TrustZone and secure monitor implementation.
- Custom kernel implementation through Mesosphère.
- Application-level Horizon OS patching through Troposphère.

### Boot and System Management

- Fusée-based first-stage firmware loading.
- Custom firmware component initialization.
- Integration with the Nintendo Switch boot architecture.
- System-level modifications during the startup process.

### Homebrew Environment

- Homebrew integration through the associated environment.
- Support for custom system modules.
- System-level extension capabilities.
- Compatibility with the Nintendo Switch homebrew ecosystem, subject to software versions.

### NAND and Configuration

- EmuMMC functionality.
- Virtualized and redirected NAND support.
- Firmware configuration management.
- Configurable system modifications and patches.

## Platform Compatibility

| Platform | Model / Revision | Firmware Version | Compatibility |
|---|---|---|---|
| Nintendo Switch | Original Switch family | 23.0.0 | Supported by Atmosphère 1.12.x |
| Nintendo Switch | Hardware revisions | Model-dependent | Verify boot-chain requirements |
| Nintendo Switch Lite | Hardware-specific configuration | Version-dependent | Verify exact requirements |
| Nintendo Switch OLED | Hardware-specific configuration | Version-dependent | Verify exact requirements |

Compatibility depends on the console's hardware revision, boot environment, firmware version, and required supporting components.

Consult the official release notes before selecting a firmware build.

## Installation and Configuration

Atmosphère requires a compatible Nintendo Switch environment and the appropriate boot components.

### Prerequisites

- Compatible Nintendo Switch hardware.
- A supported system firmware version.
- Appropriate boot configuration.
- Required Atmosphère release files.
- Compatible microSD storage.
- Relevant configuration files.

### Installation Overview

1. Identify the exact Nintendo Switch hardware revision.
2. Verify the system firmware version.
3. Review the corresponding Atmosphère release notes.
4. Prepare the required boot environment.
5. Configure the firmware components according to the official documentation.
6. Verify successful initialization.

### Configuration

Atmosphère provides configuration files for controlling selected firmware behaviors and system modules.

Configuration should be performed according to the documentation supplied with the corresponding release.

### Verification

After initialization, verify the active Atmosphère version and confirm that the expected firmware components load correctly.

## Technical Specifications

| Parameter | Details |
|---|---|
| Project | Atmosphère |
| Platform | Nintendo Switch |
| Software Type | Customized Firmware |
| System Environment | Horizon OS |
| Architecture | Layered system architecture |
| Core Components | Fusée, Exosphère, Thermosphère, Mesosphère, Stratosphère, Troposphère |
| Secondary Components | EmuMMC, Libraries |
| License | GPL-2.0 with documented exemptions |
| Repository Status | Active development |
| Official Repository | Atmosphere-NX/Atmosphere |

## Frequently Asked Questions

### What is Atmosphère?

Atmosphère is a customized firmware project for Nintendo Switch that modifies and extends multiple layers of the system software.

### Is Atmosphère a bootloader?

No. Fusée is the first-stage loader component within Atmosphère. Atmosphère itself is the broader customized firmware project.

### What is the difference between Atmosphère and Hekate?

Atmosphère provides the customized firmware environment, while Hekate is a separate bootloader and boot management project.

### Does Atmosphère support every Nintendo Switch firmware version?

No universal compatibility should be assumed. Each Atmosphère release has specific system firmware requirements and compatibility information.

### Where can I find official installation and configuration information?

Use the official Atmosphère repository, release notes, documentation, and associated project resources.

## SEO Keywords

Atmosphère custom firmware, Nintendo Switch CFW, Atmosphere firmware, Nintendo Switch system modification, Atmosphère installation, Horizon OS customization, Nintendo Switch homebrew, Fusée bootloader, Exosphère TrustZone, Mesosphère kernel, Stratosphère sysmodules, Troposphère patches, Nintendo Switch EmuMMC, custom system modules, Switch firmware architecture, Nintendo Switch firmware compatibility, Atmosphère configuration, Nintendo Switch firmware development, Horizon OS system software, Atmosphère GitHub repository.

## Technical References

- [Official Atmosphère Repository](https://github.com/Atmosphere-NX/Atmosphere)
- [Official Release History](https://github.com/Atmosphere-NX/Atmosphere/releases)
- [Atmosphère Documentation](https://github.com/Atmosphere-NX/Atmosphere/tree/master/docs)
- [Atmosphère License](https://github.com/Atmosphere-NX/Atmosphere/blob/master/LICENSE)
- [Hekate Bootloader](https://github.com/CTCaer/hekate)

<p align="center">
  <strong>Atmosphère Custom Firmware</strong>
  <br>
  Nintendo Switch · Horizon OS · System Software
  <br>
  Firmware Architecture and System-Level Development
</p>
