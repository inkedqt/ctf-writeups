---
layout: default
title: "InkSec Linux Workstation"
permalink: /Other/Arch/
---

# InkSec Linux Workstation
*CachyOS · KDE Plasma · Kitty · Black & Pink InkSec Theme*

---

## Overview
This is my daily-driver Linux workstation running **CachyOS** with  
**KDE Plasma 6**, tuned for cybersecurity labs, VMs, gaming, and long hacking sessions.

It uses my black & pink **InkSec** theme across Plasma, kitty, and wallpapers.  
Fast, aesthetic, and fully reproducible.

**Key components:**

- CachyOS (Arch-based)
- KDE Plasma 6 (Wayland)
- Kitty terminal
- VMware & KVM/QEMU support
- Dual-monitor workflow
- Custom InkSec theme and fonts

---

## Goals of the Setup

- **Fast:** snappy desktop, low latency, quick boot  
- **Reliable:** stable for CTFs, study, labs  
- **Reproducible:** easy to reinstall using notes + dotfiles  
- **Aesthetic:** consistent black/pink InkSec theme  
- **Lab-ready:** optimized for virtual machines and VPNs  
- **Clean:** minimal clutter, predictable workspaces  

---

## Hardware

**Main workstation:**

- **Motherboard:** Gigabyte B760M  
- **CPU:** Intel  
- **RAM:** 64GB  
- **Storage:** Multi-NVMe setup (Windows + CachyOS split)  
- **GPU:** NVIDIA 4070ti 
- **Monitors:** Dual-monitor Plasma layout  
- **Use case:** hacking, labs, gaming, HTB writeups  

---

## CachyOS & Base Setup

CachyOS KDE edition is the foundation.  
Then I layer tools, theming, and performance tweaks on top.

### Install Workflow

1. Install **CachyOS KDE Edition** with systemd-boot + BTRFS.
2. Update system:

       sudo pacman -Syu

3. Install base tools:

       sudo pacman -S kitty fastfetch git base-devel htop

4. Enable SDDM & networking:

       sudo systemctl enable --now sddm
       sudo systemctl enable --now NetworkManager

5. Install NVIDIA drivers + VMware / virt-manager for labs.
6. Apply InkSec theming + Plasma customisation.

---

## Plasma Layout

Plasma is my main desktop environment — after testing tiling WMs like  
Niri and Hyprland, Plasma is the most comfortable for daily work.

**My Plasma layout:**

- **Main monitor**
  - Full-width bottom panel  
  - Task manager  
  - System tray  
  - Calendar & clock  
  - App launchers  
- **Second monitor**
  - Slim micro-panel with a clock (bottom-right)
- **Workspaces**
  - Firefox profiles, code editors, and terminals remember positions
- **Theme**
  - Black background  
  - Hot pink highlight accents  
  - Matching kitty theme

Plasma gives me the best balance of stability + customisation.

---

## Kitty Terminal (InkSec Theme)

Kitty is my primary terminal — themed with black/pink InkSec colours.

**Key features:**

- JetBrainsMono Nerd Font  
- Neon pink cursor + borders  
- Transparent background option  
- Terminal “kittens” for URL hints + search  
- Fast, GPU-accelerated rendering  

**Example snippet from `~/.config/kitty/kitty.conf`:**

       font_family      JetBrainsMono Nerd Font
       background       #050507
       foreground       #EDEDED
       cursor           #FF2DAA
       background_opacity 0.92
       active_border_color   #FF2DAA
       inactive_border_color #1A1A22

---

## Screenshots

*(Paths can be changed to match your repo layout.)*

### Plasma Desktop  
![InkSec Plasma Desktop](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/Arch/desktop.png)

### Kitty Terminal  
![Kitty Theme](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/Arch/kitty.png)

### System Info (fastfetch)  
![fastfetch](https://raw.githubusercontent.com/inkedqt/ctf-writeups/main/Other/Arch/fastfetch.png)

---

## Dotfiles & Theme Downloads

All config files live in my dotfiles repo.  
These include:

- Kitty theme (`~/.config/kitty/kitty.conf`)  
- Plasma colour scheme  
- Wayland bar configs  
- SDDM + wallpapers  
- Fastfetch config  

**🔗 Dotfiles Repo:**  
https://github.com/inkedqt/inksec-dotfiles/tree/main

---

## How I Use This Setup

- **Cybersecurity labs:** Hack The Box, TryHackMe, Pro Labs, Windows AD labs  
- **Study:** Certificate IV in Cyber Security coursework  
- **CTF writeups:** Markdown writeups pushed to `inksec.io`  
- **VMs:** VMware Workstation, KVM/QEMU  
- **Gaming:** Dual boot with Windows 11  
- **Development:** Terminal workflows, website updates, scripting  

The goal is a stable, predictable workstation that feels good even after 6+ hours.

---

## Future Tweaks & Ideas

- Bundle InkSec Plasma + kitty themes into downloadable presets  
- Add a full rebuild guide for CachyOS → InkSec theme  
- Document VMware optimisations  
- Add a “Backup & dotfiles sync” section  
- Theme the SDDM login screen to match InkSec colours  

---

*Last updated: {{ site.time | date: "%B %Y" }}*
