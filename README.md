# dotfiles

Personal macOS and Arch Linux configuration. **[chezmoi](https://github.com/twpayne/chezmoi) manages config, [mpm](https://github.com/kdeldycke/meta-package-manager.git) records software, and Git stores both.** The two systems are maintained separately. Nothing here installs software or syncs config automatically.

## Layout

```text
dotfiles/
├── macos/             # macOS config: Fish, Zellij, btop, Atuin, and Git
├── linux/             # Arch Linux / Hyprland config
├── macos.toml         # macOS software inventory, mpm TOML
├── linux.toml         # Linux software inventory, currently empty
├── recipes_macos.md   # macOS export and import commands
└── recipes_linux.md   # Linux recipes, not written yet
```

- [macOS recipes](recipes_macos.md)
- [Linux recipes](recipes_linux.md)
