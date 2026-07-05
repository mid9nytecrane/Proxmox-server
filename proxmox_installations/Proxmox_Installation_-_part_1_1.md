# Proxmox Installation — Part 1: Download the Proxmox VE ISO

## Overview
This is the first step in setting up a Proxmox VE host: downloading and verifying the installer ISO before writing it to a USB drive.

## 1. Get the ISO
1. Go to the official downloads page: `https://www.proxmox.com/en/downloads/proxmox-virtual-environment`
2. Under **Proxmox VE**, download the latest ISO installer (currently **Proxmox VE 9.2**, based on Debian 13 "Trixie", ~1.7 GB).
3. Save it somewhere easy to find, e.g. `~/Downloads/proxmox-ve_9.2-1.iso`.

> Alternate mirror (if the main site is slow): `https://enterprise.proxmox.com/iso`

## 2. Verify the checksum
Always verify the download before using it — a corrupted or tampered ISO can cause failed installs or worse.

1. Copy the **SHA256SUM** value shown next to the ISO on the download page.
2. Run the checksum locally:
   ```bash
   sha256sum proxmox-ve_9.2-1.iso
   ```
3. Compare the output to the published checksum — they must match exactly.

## 3. Requirements before moving to Part 2
- A USB stick **4 GB or larger**.
- CPU virtualization extensions (**Intel VT-x** or **AMD-V**) enabled in BIOS/UEFI — required for VMs to run at all.
- A tool to write the ISO to USB in **DD/raw mode**, e.g. `dd`, Balena Etcher, or Rufus (Rufus must be set to DD mode, not ISO mode — UNetbootin does not work with this image).

## Notes
- Fixed: original file only had the heading with no supporting steps — this version adds the actual download, verification, and pre-install checklist.
- Next: **Part 2** should cover writing the ISO to USB and running the installer (disk/filesystem choice, network config, root password).
