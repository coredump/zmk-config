# ZMK Config

Personal [ZMK firmware](https://github.com/zmkfirmware/zmk/) configuration for the Crosses split keyboard with trackball support.

The configuration builds against ZMK `v0.3`, extended by various ZMK modules. All build dependencies are pinned in the [`west` manifest](config/west.yml).

> **Note:** This configuration is based on [urob's zmk-config](https://github.com/urob/zmk-config). Refer to that repository for detailed explanations of the keymap features (timeless homerow mods, combos, smart layers, etc.). Parts of this README were updated with the assistance of an AI agent (Claude).

## Highlights

- "Timeless" homerow mods
- Combos instead of symbol layer
- Auto-toggle off numbers and mouse layers
- Magic thumb quadrupling as Repeat/Sticky-shift/Capsword/Shift
- Leader key sequences for Unicode input and system commands
- Trackball with scroll snapping

![](draw/crosses.svg)

(Powered by [keymap-drawer](https://github.com/caksoylar/keymap-drawer).)

## Local build environment

The build process uses `nix`, `direnv` and `just` to automatically set up a virtual development environment with `west`, the `zephyr-sdk` and all dependencies. The environment is completely isolated and won't pollute your system.

### Pre-requisites

1. Install the `nix` package manager:

   ```bash
   curl --proto '=https' --tlsv1.2 -sSf -L https://install.determinate.systems/nix |
      sh -s -- install --no-confirm

   . /nix/var/nix/profiles/default/etc/profile.d/nix-daemon.sh
   ```

2. Install [`direnv`](https://direnv.net/) and optionally [`nix-direnv`](https://github.com/nix-community/nix-direnv):

   ```bash
   nix profile install nixpkgs#direnv nixpkgs#nix-direnv
   ```

3. Set up the `direnv` [shell-hook](https://direnv.net/docs/hook.html) for your shell.

### Setup

1. Clone this repository:

   ```bash
   git clone <your-repo-url> zmk-workspace
   ```

2. Enter the workspace and set up the environment:

   ```bash
   cd zmk-workspace
   direnv allow
   just init
   ```

### Usage

```
zmk-workspace
├── config
├── firmware (created after building)
├── modules
├── zephyr
└── zmk
```

#### Building

```bash
just build all          # Build all targets in build.yaml
just build crosses      # Build Crosses keyboard (left + right)
just list               # List all valid build targets
just build all -p       # Pristine build
just clean              # Clear build cache
```

#### Drawing the keymap

```bash
just draw               # Generates draw/crosses.svg
```

#### Updating

```bash
just update             # Update ZMK and modules from west.yml
just upgrade-sdk        # Upgrade Zephyr SDK (use with care)
```

## Related resources

- ZMK modules used in this configuration are in `modules/zmk/`
- [ZMK Documentation](https://zmk.dev/docs)
- [urob's zmk-config](https://github.com/urob/zmk-config) - Original configuration with detailed feature explanations
