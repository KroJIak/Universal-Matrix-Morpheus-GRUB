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

| Distribution | Icons in `Matrix/icons/` |
|--------------|--------------------------|
| Arch Linux   | `arch_on.png`, `arch_off.png` |
| Debian       | `debian_on.png`, `debian_off.png` |
| Ubuntu       | `ubuntu_on.png`, `ubuntu_off.png` |

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
   git clone https://github.com/YOUR_USER/Universal-Matrix-Morpheus-GRUB
   cd Universal-Matrix-Morpheus-GRUB
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
   - **1) Auto-detect** — Automatically detect the distribution
   - **2) Select manually** — Choose the distribution by number from the list

5. Reboot to see the theme.

---

## Icon Selection Logic

1. Distributions are read from `distros.conf` in priority order (top to bottom)
2. A substring match is performed against `GRUB_DISTRIBUTOR` / `ID` from `/etc/os-release`
3. Presence of `{name}_on.png` and `{name}_off.png` in `Matrix/icons/` is checked
4. If a match is found — those icons are used
5. If not — `assets/linux_template.png` is used as fallback

If only Windows is installed (no Linux), `linux_template.png` is used as a non-booting placeholder and `windows_template.png` for booting Windows. If neither OS is found, both options remain placeholders.

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
│   ├── linux.psd
│   └── windows.psd
├── distros.conf        # Distribution config and priorities
├── install.sh
└── README.md
```

`os_linux.png` and `os_windows.png` are empty placeholder files. Menu icons are taken from `Matrix/icons/` by class (`arch`, `debian`, `ubuntu`, `windows`, etc.) and prepared by the install script.

---

## Simplifying the GRUB Menu

The theme works best with a minimal menu (e.g. one Linux and one Windows entry). Extra entries like "Advanced options" or "UEFI Firmware Settings" can be disabled in `/etc/default/grub` or in scripts under `/etc/grub.d/`.

---

## Fork

Universal version based on [Matrix-Morpheus-GRUB-Theme](https://github.com/Priyank-Adhav/Matrix-Morpheus-GRUB-Theme) with support for multiple distributions.
