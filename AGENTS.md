# ZMK Workspace - Agent Configuration

## Project Overview

ZMK firmware configuration for split keyboards with trackball support. Uses mise/uv/just/west build system.

## Keyboards

- **Crosses** - 36-key split, Nice!Nano v2, PMW3610 trackball, OLED displays
- **Prospector Scanner** - Xiao BLE display module

## Build Commands

```bash
just setup              # First-time setup (venv, SDK, deps)
just init               # Initialize west workspace
just build crosses      # Build Crosses (left + right)
just build prospector   # Build Prospector Scanner
just build all          # Build all targets
just build all -p       # Pristine build
just draw               # Generate keymap SVG
just update             # Update west dependencies
just clean              # Clear build artifacts
```

## Key Directories

- `config/` - Keyboard configuration (keymaps, combos, conf files)
- `draw/` - Keymap visualization (config.yaml, output SVGs)
- `firmware/` - Compiled .uf2 files (gitignored)
- `.build/` - Build artifacts (gitignored)
- `gggw-zmk-keebs/` - Hardware definitions (fetched by west)
- `modules/zmk/` - ZMK community modules (helpers, adaptive-key, etc.)

## Configuration Files

- `config/base.keymap` - Shared keymap definitions
- `config/crosses.keymap` - Crosses-specific keymap (includes base.keymap)
- `config/crosses.conf` - Crosses ZMK settings
- `config/combos.dtsi` - Combo definitions
- `config/mouse.dtsi` - Trackball configuration
- `config/west.yml` - West manifest (dependencies)
- `build.yaml` - Build target matrix

## Keymap Conventions

- Uses urob's zmk-helpers for key labels (36-key layout)
- Homerow mods on GACS (GUI, Alt, Ctrl, Shift)
- Layers: BASE, MAC, GAMING, LOWER, RAISE, ADJUST, MOUSE, NUM, NAV, MACNAV, SNIPE, WARP, SCROLL
- Combos defined in combos.dtsi using helper macros

## ZMK Modules in Use

- zmk-helpers - Key position helpers
- zmk-adaptive-key - Adaptive behaviors
- zmk-auto-layer - Auto layer toggle
- zmk-leader-key - Leader sequences
- zmk-tri-state - Tri-state behaviors
- zmk-scroll-snap - macOS scroll snapping
- zmk-pmw3610-driver - Trackball sensor
- zmk-rgbled-widget - RGB status LED

## Notes

- Right half has ZMK Studio enabled (USB connection required)
- Trackball layers: MOUSE (default), SNIPE (precision), SCROLL (scrolling)
- Build outputs go to `firmware/` as .uf2 files
