# macOS recipes

- [macOS recipes](#macos-recipes)
  - [Export dotfiles with chezmoi](#export-dotfiles-with-chezmoi)
  - [Export software with mpm](#export-software-with-mpm)
  - [Import dotfiles with chezmoi](#import-dotfiles-with-chezmoi)
  - [Import software with mpm](#import-software-with-mpm)

Run these commands from the repository root.

## Export dotfiles with [chezmoi](https://github.com/twpayne/chezmoi)

Delete everything under `macos/` except `.chezmoiignore`.

```sh
find macos -mindepth 1 ! -name '.chezmoiignore' -delete
```

Write the local config into `macos/`.

```sh
chezmoi --source "$PWD/macos" --working-tree "$PWD" add --secrets=error \
  ~/.gitconfig \
  ~/.config/fish/config.fish \
  ~/.config/fish/conf.d/atuin.env.fish \
  ~/.config/fish/conf.d/uv.env.fish \
  ~/.config/zellij/config.kdl \
  ~/.config/btop/btop.conf \
  ~/.config/atuin/config.toml \
  ~/.config/git/ignore
```

## Export software with [mpm](https://github.com/kdeldycke/meta-package-manager.git)

Dump the selected managers to `tmp/macos.toml`.

```sh
mpm --no-config --stop-on-error --jobs 1 --timeout 30 --brew --cask --npm --cargo --uvx dump --overwrite tmp/macos.toml
```

Review the diff, then replace `macos.toml`.

```sh
git diff --no-index -- macos.toml tmp/macos.toml
```

```sh
mv tmp/macos.toml macos.toml
```

## Import dotfiles with chezmoi

Preview the diff.

```sh
chezmoi --source "$PWD/macos" --working-tree "$PWD" diff
```

Apply it.

```sh
chezmoi --source "$PWD/macos" --working-tree "$PWD" apply
```

## Import software with mpm

```sh
mpm restore macos.toml
```
