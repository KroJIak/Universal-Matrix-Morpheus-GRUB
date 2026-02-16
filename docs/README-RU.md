[English](../README.md) | [Русский](README-RU.md)

<div align="center">

![Bash](https://img.shields.io/badge/Bash-5.0+-4EAA25?style=for-the-badge&logo=gnu-bash&logoColor=white)
![GRUB](https://img.shields.io/badge/GRUB-bootloader-CE2B2B?style=for-the-badge&logo=gnu&logoColor=white)
![Arch](https://img.shields.io/badge/Arch-supported-1793D1?style=for-the-badge&logo=arch-linux&logoColor=white)
![Debian](https://img.shields.io/badge/Debian-supported-A81D33?style=for-the-badge&logo=debian&logoColor=white)
![Ubuntu](https://img.shields.io/badge/Ubuntu-supported-E95420?style=for-the-badge&logo=ubuntu&logoColor=white)
![Linux](https://img.shields.io/badge/Linux%20%7C%20Windows-multiboot-FCC624?style=for-the-badge&logo=linux&logoColor=black)

</div>

# Matrix Morpheus GRUB Theme (Universal)

**Red Pill vs Blue Pill** — минималистичная GRUB‑тема в стиле «Матрицы» с полноэкранными иконками выбора ОС.

---

## Поддерживаемые дистрибутивы

Тема автоматически определяет дистрибутив и подставляет нужные иконки. Из коробки поддерживаются:

| Дистрибутив | Иконки в `Matrix/icons/` |
|-------------|--------------------------|
| Arch Linux  | `arch_on.png`, `arch_off.png` |
| Debian      | `debian_on.png`, `debian_off.png` |
| Ubuntu      | `ubuntu_on.png`, `ubuntu_off.png` |

### Добавление своего дистрибутива

1. Создайте иконки `{name}_on.png` и `{name}_off.png` в `Matrix/icons/`
2. Добавьте строку в `distros.conf`:
   ```
   keyword|icon_on|icon_off
   ```
   Например для Fedora: `fedora|fedora_on.png|fedora_off.png`
3. Ключевое слово (keyword) сопоставляется по подстроке с `GRUB_DISTRIBUTOR` и `ID` из `/etc/os-release`

### Шаблоны для своих иконок

В папке `assets/` находятся шаблоны для самостоятельной доработки:

- `linux_template.png` — базовая картинка для Linux (красная пилюля)
- `windows_template.png` — базовая картинка для Windows (синяя пилюля)
- `linux.psd`, `windows.psd` — исходники для Photoshop

Эти шаблоны используются как fallback, если для вашего дистрибутива нет готовых иконок.

---

## Установка

1. Клонируйте репозиторий:
   ```bash
   git clone https://github.com/YOUR_USER/Universal-Matrix-Morpheus-GRUB
   cd Universal-Matrix-Morpheus-GRUB
   ```

2. Сделайте скрипт исполняемым:
   ```bash
   chmod +x install.sh
   ```

3. Запустите установку от root:
   ```bash
   sudo ./install.sh
   ```

4. При установке будет предложено:
   - **1) Auto-detect** — автоматически определить дистрибутив
   - **2) Select manually** — вручную выбрать номер дистрибутива из списка

5. Перезагрузитесь, чтобы увидеть тему.

---

## Логика выбора иконок

1. Берётся список дистрибутивов из `distros.conf` (сверху вниз по приоритету)
2. По подстроке ищется совпадение с `GRUB_DISTRIBUTOR` / `ID` из `/etc/os-release`
3. Проверяется наличие `{name}_on.png` и `{name}_off.png` в `Matrix/icons/`
4. Если совпадение найдено — используются эти иконки
5. Если нет — берётся `assets/linux_template.png` как запасной вариант

Если установлена только Windows (нет Linux), используется `linux_template.png` как заглушка, а `windows_template.png` — для запуска Windows. При отсутствии обеих ОС обе кнопки остаются заглушками.

---

## Структура проекта

```
├── Matrix/
│   ├── theme.txt       # Конфигурация темы GRUB
│   ├── font.pf2        # Шрифт
│   ├── icons/          # Иконки дистрибутивов (_on / _off)
│   ├── os_linux.png    # Пустой placeholder (legacy)
│   └── os_windows.png  # Пустой placeholder (legacy)
├── assets/
│   ├── linux_template.png
│   ├── windows_template.png
│   ├── linux.psd
│   └── windows.psd
├── distros.conf        # Конфигурация дистрибутивов и приоритетов
├── install.sh
└── README.md
```

`os_linux.png` и `os_windows.png` — пустые placeholder-файлы. Иконки для меню GRUB берутся из `Matrix/icons/` по классам (`arch`, `debian`, `ubuntu`, `windows` и т.д.) и подготавливаются скриптом установки.

---

## Упрощение меню GRUB

Тема рассчитана на минимальное меню (например, одна Linux и одна Windows). Лишние пункты вроде «Advanced options» или «UEFI Firmware Settings» можно отключить в `/etc/default/grub` или в скриптах в `/etc/grub.d/`.

---

## Форк

Универсальная версия на основе [Matrix-Morpheus-GRUB-Theme](https://github.com/Priyank-Adhav/Matrix-Morpheus-GRUB-Theme) с поддержкой нескольких дистрибутивов.
