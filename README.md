
 # Cisco Catalyst 2960-X | Secure Sanitization & IOS Restoration
<p align="center">
  <img src="assets/brandons-logo.png" alt="Brandon Stevenson IT Professional" width="300">
</p>

### NIST-Aligned Secure Sanitization • Cisco IOS Recovery • Boot Configuration • Post-Reimage Verification



---


## Overview

This repository documents the sanitization, Cisco IOS recovery, and boot configuration of a physical Cisco Catalyst WS-C2960X-24TS-L access switch.

The procedure was carried out through a serial-console connection using Tera Term, with direct access to the Cisco bootloader and IOS command-line interface.

Work included internal flash formatting, secure factory-reset operations, FIPS zeroization, USB-based IOS recovery, installation of the operating-system image to internal flash, and boot configuration.

The switch was subsequently inspected through IOS commands to review its configuration, VLAN database, VTP status, power capability, and hardware inventory.

### Recovery Workflow

<p align="center">
  <img src="assets/flowchart.png"
       alt="Cisco Catalyst 2960-X Infrastructure Recovery and Sanitization Flowchart"
       width="100%">
</p>

The repository includes 12 CLI evidence captures, equipment photographs, and a supporting technical report. Sanitization activities were performed under NIST-aligned equipment-processing procedures; the published evidence documents device operations rather than formal sanitization acceptance.


| Project Detail | Information |
|---|---|
| Hardware | Cisco Catalyst WS-C2960X-24TS-L |
| Operating System | Cisco IOS |
| IOS Image | `c2960x-universalk9-mz.152-7.E11.bin` |
| Console Application | Tera Term |
| Access Method | Serial Console |
| Recovery Media | USB Flash Drive |
| Environment | Isolated Physical Equipment |
| Sanitization Framework | NIST-aligned organizational procedures |

---

## Table of Contents

- [Equipment Photos](#equipment-photos)
- [Hardware and Tools](#hardware-and-tools)
- [Work Completed](#work-completed)
- [Sanitization Standards](#sanitization-standards)
- [Recovery Workflow](#recovery-workflow)
- [CLI Walkthrough](#cli-walkthrough)
  - [Phase 01 — Flash Formatting](#phase-01)
  - [Phase 02 — IOS Boot from USB](#phase-02)
  - [Phase 03 — Secure Factory Reset](#phase-03)
  - [Phase 04 — FIPS Zeroization](#phase-04)
  - [Phase 05 — Bootloader Inspection](#phase-05)
  - [Phase 06 — Post-Zeroization IOS Boot](#phase-06)
  - [Phase 07 — IOS Installation and Boot Configuration](#phase-07)
  - [Phase 08 — Running Configuration](#phase-08)
  - [Phase 09 — Startup Configuration](#phase-09)
  - [Phase 10 — VLAN Inspection](#phase-10)
  - [Phase 11 — VTP and Power Inspection](#phase-11)
  - [Phase 12 — Hardware Inventory](#phase-12)
- [Verification Summary](#verification-summary)
- [Project Files](#project-files)
- [About](#about)

---

## Equipment Photos

### Cisco Catalyst 2960-X — Full Switch

<p align="center">
  <img src="assets/c2960x-whole.png" alt="Cisco Catalyst 2960-X physical switch" width="750">
</p>

*Cisco Catalyst 2960-X enterprise access switch used in this project.*

### Front Panel and SFP Uplinks

<p align="center">
  <img src="assets/c2960x-front.png" alt="Cisco Catalyst 2960-X front panel and SFP uplink ports" width="750">
</p>

*Front-panel view showing the Gigabit Ethernet interfaces and SFP uplink ports.*

*Equipment photo backgrounds were digitally modified for presentation. CLI screenshots document the actual switch operations.*

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

## Hardware and Tools

| Component | Details |
|---|---|
| Manufacturer | Cisco Systems |
| Switch | Catalyst WS-C2960X-24TS-L |
| Switch Type | Layer 2 Enterprise Access Switch |
| Ethernet Ports | 24 × 10/100/1000 |
| Uplink Ports | 4 × 1G SFP |
| PoE Support | Non-PoE Model |
| Operating System | Cisco IOS |
| IOS Image | `c2960x-universalk9-mz.152-7.E11.bin` |
| Terminal Software | Tera Term |
| Device Connection | Serial Console |
| Recovery Environment | Cisco Bootloader |
| Installation Media | USB Flash Drive |
| Work Environment | Isolated Physical Switch |

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

## Work Completed

The following operations were performed and recorded during the switch sanitization and reimaging process:

- Connected to the physical switch using a serial-console connection.
- Accessed the Cisco bootloader environment.
- Inspected and formatted internal flash storage.
- Performed authorized secure factory-reset and FIPS zeroization commands.
- Booted Cisco IOS directly from a USB flash drive.
- Reinstalled the IOS image into internal flash.
- Configured the boot image and inspected the boot settings.
- Reviewed running and startup configurations.
- Checked VLAN and VTP information.
- Inspected the switch's power capability.
- Confirmed the hardware model through Cisco IOS inventory output.
- Documented the process with 12 CLI screenshots.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

## Sanitization Standards

The equipment-processing environment follows NIST media sanitization standards, including procedures aligned with **NIST SP 800-88**.

The documented switch operations included secure factory reset, cryptographic zeroization, flash storage management, and post-operation configuration inspection.

Following sanitization, Cisco IOS was reinstalled to internal flash and the switch's boot configuration was inspected.

The screenshots in this repository record the technical operations performed. They do not replace the organization's formal sanitization verification or acceptance records.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

## Recovery Workflow

```mermaid
flowchart TD
    A["Physical Cisco Catalyst 2960-X"] --> B["Serial Console / Bootloader"]
    B --> C["Flash Inspection and Formatting"]
    C --> D["Boot IOS from USB"]
    D --> E["Secure Factory Reset"]
    E --> F["FIPS Zeroization"]
    F --> G["Boot IOS from USB Again"]
    G --> H["Copy IOS to Internal Flash"]
    H --> I["Configure and Inspect Boot Settings"]
    I --> J["Inspect Running and Startup Configurations"]
    J --> K["Verify VLAN, VTP and Hardware Inventory"]
```

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

## CLI Walkthrough

The following screenshots document the switch operations performed during sanitization, IOS reinstallation, and post-reimage inspection.

Hardware serial numbers, MAC addresses, and sensitive device identifiers have been redacted where identified in the published evidence.

---

<a id="phase-01"></a>

### Phase 01 — Flash Formatting

**Commands**

```text
format flash:
dir flash:
```

Accessed the internal flash filesystem through the Cisco bootloader.

Formatted internal flash and inspected the directory contents afterward.

The directory listing was used to review the filesystem state before proceeding with the recovery sequence.

**CLI Evidence**

![Phase 01 — Flash Formatting](evidence/2960x-step1.png)

**Verification:** The bootloader confirmed that flash formatting completed. The subsequent directory listing showed no files.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-02"></a>

### Phase 02 — IOS Boot from USB

**Command**

```text
boot usbflash0:c2960x-universalk9-mz.152-7.E11.bin
```

Loaded Cisco IOS directly from the USB recovery image through the bootloader.

This provided access to the IOS operating environment after internal flash handling.

**CLI Evidence**

![Phase 02 — IOS Boot from USB](evidence/2960x-step2.png)

**Evidence:** The bootloader loaded the specified IOS image from USB and reported that digital-signature verification passed.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-03"></a>

### Phase 03 — Secure Factory Reset

**Command**

```text
factory-reset all secure
```

Executed the authorized secure factory-reset command as part of the equipment sanitization process.

The terminal displayed the reset confirmation and information about the data targeted by the operation.

**CLI Evidence**

![Phase 03 — Secure Factory Reset](evidence/2960x-step3.png)

**Evidence:** The console displayed the secure factory-reset confirmation prompt and identified the files and configuration data targeted for deletion.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-04"></a>

### Phase 04 — FIPS Zeroization

**Commands**

```text
configure terminal
fips zeroize
```


Issued `fips zeroize` from global configuration mode and confirmed the operation through all three console prompts.

The switch initiated the zeroization process and subsequently reloaded. During execution, the console also reported `FIPS: Error removing authorization-key.`

The captured output documents the zeroization attempt and resulting system response, but does not independently confirm complete removal of all cryptographic material.


**CLI Evidence**

![Phase 04 — FIPS Zeroization](evidence/2960x-step4.png)

**Evidence:** The zeroization command was initiated, but the console reported an authorization-key removal error before the subsequent reload.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-05"></a>

### Phase 05 — Bootloader Inspection

**Commands**

```text
set
dir usbflash0:
```


Used `set` to inspect the bootloader environment and identify the switch's hardware and boot settings.

Executed `dir usbflash0:` to confirm access to the attached USB storage and inspect its available firmware images.

The bootloader identified the hardware as `WS-C2960X-24TS-L`. The subsequent recovery-image boot is documented separately in Phase 06.


**CLI Evidence**

![Phase 05 — Bootloader Inspection](evidence/2960x-step5.png)

**Evidence:** Bootloader variables identified the switch model, and the USB directory listing confirmed access to recovery media.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-06"></a>

### Phase 06 — Post-Zeroization IOS Boot

**Command**

```text
boot usbflash0:c2960x-universalk9-mz.152-7.E11.bin
```

Booted Cisco IOS from the USB flash drive again after the sanitization and zeroization operations.

This restored access to IOS for reinstalling the image into internal flash.

**CLI Evidence**

![Phase 06 — Post-Zeroization IOS Boot](evidence/2960x-step6.png)

**Evidence:** The second USB-based image load passed digital-signature verification.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-07"></a>

### Phase 07 — IOS Installation and Boot Configuration

**IOS Image Transfer**

```text
copy usbflash0: flash:
```

**IOS Image**

`c2960x-universalk9-mz.152-7.E11.bin`

**Boot Configuration**

```text
configure terminal
boot system flash:c2960x-universalk9-mz.152-7.E11.bin
end
copy running-config startup-config
show boot
```

Copied the Cisco IOS image from USB media into the switch's internal flash storage.

Configured the boot statement to reference the installed IOS image and saved the running configuration.

Used `show boot` to inspect the configured boot path.

**CLI Evidence**

![Phase 07 — IOS Installation and Boot Configuration](evidence/2960x-step7.png)

**Verification:** The 26,797,056-byte IOS image copy completed, the startup configuration was saved, and the configured boot path pointed to the installed image.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-08"></a>

### Phase 08 — Running Configuration

**Command**

```text
show running-config
```

Inspected the active Cisco IOS configuration following reinstallation.

The running configuration was reviewed for existing device settings and configuration information.

**CLI Evidence**

![Phase 08 — Running Configuration](evidence/2960x-step8.png)

**Evidence:** The running configuration displayed the Switch hostname, IOS configuration settings, and switch provisioning information.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-09"></a>

### Phase 09 — Startup Configuration

**Command**

```text
show startup-config
```

Inspected the saved startup configuration following IOS reinstallation.

The startup configuration was reviewed separately from the running configuration to confirm the saved device state.

**CLI Evidence**

![Phase 09 — Startup Configuration](evidence/2960x-step9.png)

**Evidence:** The startup configuration was present in NVRAM and displayed the saved 1,650-byte configuration.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-10"></a>

### Phase 10 — VLAN Inspection

**Command**

```text
show vlan
```

Inspected the switch's VLAN database following the reimage.

The captured output displayed default VLAN information, including VLAN 1 and the reserved VLAN entries.

**CLI Evidence**

![Phase 10 — VLAN Inspection](evidence/2960x-step10.png)

**Evidence:** The VLAN database contained VLAN 1 and the reserved default VLANs 1002–1005, with no custom VLANs shown.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-11"></a>

### Phase 11 — VTP and Power Inspection

**Commands**

```text
show vtp status
show power inline
```

Reviewed the switch's VLAN Trunking Protocol configuration and power-delivery capability.

The VTP output provided information about the switch's VLAN management state.

The WS-C2960X-24TS-L is a non-PoE model, so PoE functionality is not supported.

**CLI Evidence**

![Phase 11 — VTP and Power Inspection](evidence/2960x-step11.png)

**Evidence:** VTP reported server mode with configuration revision 0. Inline power values were unavailable, consistent with the non-PoE switch model
 
<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

<a id="phase-12"></a>

### Phase 12 — Hardware Inventory

**Command**

```text
show inventory
```

Inspected the hardware inventory to confirm the physical switch model.

The output identified the equipment as a **Cisco Catalyst WS-C2960X-24TS-L**.

Device serial-number information was redacted from the published screenshot.

**CLI Evidence**

![Phase 12 — Hardware Inventory](evidence/2960x-step12.png)

**Verification:** The inventory output identified PID WS-C2960X-24TS-L. The device serial number was redacted from the published capture.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---


## Verification Summary

The following results are supported by the published serial-console evidence.

| Verification Item | Documented Finding |
|---|---|
| Physical device access | Serial-console access established |
| Bootloader access | Environment variables inspected |
| Internal flash formatting | Filesystem formatting confirmed |
| USB recovery media | USB directory inspected |
| IOS image loading | Digital-signature verification passed |
| Secure factory reset | Command and confirmation output captured; full completion not independently verified |
| FIPS zeroization | Operation initiated; authorization-key removal error reported |
| IOS image installation | 26,797,056 bytes copied to internal flash |
| Boot configuration | BOOT path-list displayed the installed IOS image |
| Configuration persistence | Startup configuration saved successfully |
| Running configuration | Inspected through `show running-config` |
| Startup configuration | Inspected through `show startup-config` |
| VLAN database | Default VLANs identified |
| VTP configuration | Server mode, revision 0 |
| Power capability | Non-PoE model; inline power unavailable |
| Hardware identification | WS-C2960X-24TS-L confirmed |
| Independent reboot from internal flash | Not documented |
| Physical interface connectivity | Not tested in the published evidence |
| Formal sanitization acceptance | Outside the scope of the published record |

### Verification Scope

The console captures establish the documented recovery and configuration activities. They do not constitute a formal sanitization certificate, and no claim is made that post-recovery interface functionality or independent boot validation was completed beyond the available evidence.


<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

## Project Files

### Technical Report

[View Technical Project Report (PDF)](Cisco_2960X_Sanitation%2BReimage.pdf)

### Repository Structure

```text
Cisco-Catalyst-2960X-Hands-On-Infrastructure-Project/
│
├── README.md
│
├── Cisco_2960X_Sanitation+Reimage.pdf
│
├── assets/
│   ├── brandons-logo.png
│   ├── c2960x-whole.png
│   └── c2960x-front.png
│
└── evidence/
    ├── 2960x-step1.png
    ├── 2960x-step2.png
    ├── 2960x-step3.png
    ├── 2960x-step4.png
    ├── 2960x-step5.png
    ├── 2960x-step6.png
    ├── 2960x-step7.png
    ├── 2960x-step8.png
    ├── 2960x-step9.png
    ├── 2960x-step10.png
    ├── 2960x-step11.png
    └── 2960x-step12.png
```

The `assets/` directory contains the equipment photographs and branding.

The `evidence/` directory contains the terminal screenshots from each documented phase.

The PDF provides a separate technical record of the sanitization and IOS reinstallation process.

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>

---

## About

I'm Brandon Stevenson, an IT Profesional working with enterprise server and network equipment.


This repository documents one of my hands-on infrastructure projects using physical enterprise networking hardware.

**Portfolio:** [brandons-resume.com](https://brandons-resume.com)

**GitHub:** [Programmer-stevenson](https://github.com/Programmer-stevenson)

**LinkedIn:** [Brandon Stevenson](https://www.linkedin.com/in/brandon-in-tech/)

---

*This project documents technical operations performed on enterprise equipment. The repository is not an official sanitization certificate.*

<p align="right">
  <a href="#table-of-contents">↑ Back to Table of Contents</a>
</p>
