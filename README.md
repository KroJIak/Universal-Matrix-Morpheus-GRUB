[English](README.md) | [Русский](docs/README-RU.md)

<div align="center">

![Bash](https://img.shields.io/badge/Bash-5.0+-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![GRUB](https://img.shields.io/badge/GRUB-bootloader-CE2B2B?style=for-the-badge&logo=gnu&logoColor=white)
![Arch](https://img.shields.io/badge/Arch-supported-1793D1?style=for-the-badge&logo=arch-linux&logoColor=white)
![Debian](https://img.shields.io/badge/Debian-supported-A81D33?style=for-the-badge&logo=debian&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-supported-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Linux](https://img.shields.io/badge/Linux%20%7C%20Windows-multiboot-FCC624?style=for-the-badge&logo=linux&logoColor=black)

</div>

# Matrix Morpheus GRUB Theme (Universal)

**Red Pill vs Blue Pill** — A minimalist Matrix-inspired GRUB theme with full-screen OS selection icons.

---

## Supported Distributions

The theme auto-detects your distribution and applies the matching icons. Supported out of the box:

| | |
|:-------:|:-------:|
|<img src="Matrix/icons/debian_on.png" width="247"><br><img src="Matrix/icons/debian_off.png" width="247">|**Debian** — `debian_on.png` / `debian_off.png`|
|<img src="Matrix/icons/arch_on.png" width="247"><br><img src="Matrix/icons/arch_off.png" width="247">|**Arch** — `arch_on.png` / `arch_off.png`|
|<img src="Matrix/icons/ubuntu_on.png" width="247"><br><img src="Matrix/icons/ubuntu_off.png" width="247">|**Ubuntu** — `ubuntu_on.png` / `ubuntu_off.png`|
|<img src="assets/linux_template.png" width="247"><br><img src="assets/windows_template.png" width="247">|**Templates** — `linux_template.png` / `windows_template.png`|

### Adding Your Own Distribution

1. Create `{name}_on.png` and `{name}_off.png` in `Matrix/icons/`
2. Add a line to `distros.conf`:
   ```
   keyword|icon_on|icon_off
   ```
   Example for Fedora: `fedora|fedora_on.png|fedora_off.png`
3. The keyword is matched as a substring against `GRUB_DISTRIBUTOR` and `ID` from `/etc/os-release`

### Icon Templates

The `assets/` folder contains templates for custom edits:

- `linux_template.png` — Base image for Linux (red pill)
- `windows_template.png` — Base image for Windows (blue pill)
- `linux.psd`, `windows.psd` — Photoshop source files

These templates are used as fallback when no dedicated icons exist for your distribution.

---

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/KroJIak/universal-matrix-morpheus-grub
   cd universal-matrix-morpheus-grub
   ```

2. Make the script executable:
   ```bash
   chmod +x install.sh
   ```

3. Run the installer as root:
   ```bash
   sudo ./install.sh
   ```

4. During installation you will be asked:
   - **Screen resolution** — HD, Full HD, 2K, or 4K (fixes small/big loader on high-DPI displays)
   - **Linux/Windows identification** — Only if auto-detect fails: which menu entry is Linux and which is Windows
   - **Distribution for icons** — Only if the Linux distro wasn't found: select from the list

5. **Important:** The theme is designed for exactly **2 boot entries** (e.g. your Linux distro + Windows). If you have more (UEFI Settings, Advanced options, etc.), the installer will explain how to reduce them.

6. The installer also hides the brief blue Debian/Ubuntu loading screen and "Loading Linux..." text during boot, using a black background and quiet mode.

7. Reboot to see the theme.

---

## Icon Selection Logic

After confirming there are only 2 boot entries, the script auto-detects everything:

1. **Linux vs Windows** — Identifies which menu entry is Linux and which is Windows (by GRUB classes and titles)
2. **Linux distro** — Matches against `distros.conf` (entry classes, titles, and `/etc/os-release`)
3. Questions are asked **only when auto-detect fails**: which entry is Linux/Windows, or which distro icons to use
4. Fallback: `assets/linux_template.png` if no distro match is found

If only Windows is installed, `linux_template.png` is used as a non-booting placeholder and `windows_template.png` for Windows.

---

## Project Structure

```
├── Matrix/
│   ├── theme.txt       # GRUB theme config
│   ├── font.pf2        # Font
│   ├── icons/          # Distribution icons (_on / _off)
│   ├── os_linux.png    # Empty placeholder (legacy)
│   └── os_windows.png  # Empty placeholder (legacy)
├── assets/
│   ├── linux_template.png
│   ├── windows_template.png
│   ├── black.png            # 1x1 black pixel for boot transition
│   ├── linux.psd
│   └── windows.psd
├── distros.conf        # Distribution config and priorities
├── install.sh
└── README.md
```

`os_linux.png` and `os_windows.png` are empty placeholder files. Menu icons are taken from `Matrix/icons/` by class (`arch`, `debian`, `ubuntu`, `windows`, etc.) and prepared by the install script.

---

## Simplifying the GRUB Menu

The theme works **only with 2 boot entries** — one for Linux, one for Windows. If you have more entries (e.g. "Advanced options", "UEFI Firmware Settings", multiple distros), the installer will exit and explain how to reduce them. Edit `/etc/default/grub` and scripts in `/etc/grub.d/`, then run `update-grub` and try again.

---

## Fork

Universal version based on [Matrix-Morpheus-GRUB-Theme](https://github.com/Priyank-Adhav/Matrix-Morpheus-GRUB-Theme) with support for multiple distributions.
