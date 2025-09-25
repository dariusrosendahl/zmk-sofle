# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a ZMK (Zephyr Mechanical Keyboard) configuration repository for a Sofle keyboard with customizations including:
- Mouse movement and scrolling support via rotary encoder
- RGB lighting controls
- Home row mods (GUI/Alt/Ctrl/Shift on ASDF/JKL; keys)
- Layer-tap behaviors for space and caps lock
- Bluetooth device switching
- Nice View display support

## Key Architecture

### File Structure
- `config/sofle.keymap` - Main keymap definition with 4 layers and custom behaviors
- `config/sofle.json` - Physical keyboard layout definition for keymap visualization
- `config/west.yml` - ZMK module dependencies and versions
- `config/boards/` - Hardware-specific device tree files (.dts, .dtsi, .overlay)
- `build.yaml` - Build configuration specifying which boards/shields to build
- `keymap_drawer.config.yaml` - Keymap visualization styling configuration

### Layer Architecture
- **Layer 0**: Base QWERTY with home row mods
- **Layer 1**: Navigation, function keys, mouse movement (accessed via space hold)
- **Layer 2**: System controls, RGB, Bluetooth, bootloader (accessed via caps hold)  
- **Layer 3**: Empty placeholder layer

### Custom Behaviors
The keymap defines several hold-tap behaviors in `config/sofle.keymap:22-83`:
- `hm_l`/`hm_r` - Home row mods with 250ms tapping term
- `spc_layer` - Space tap / Layer 1 hold
- `caps_layer2` - Caps tap / Layer 2 hold
- `mmv`/`msc` - Mouse movement and scroll with custom acceleration

## Development Commands

### Building Firmware
Firmware builds automatically via GitHub Actions when pushing changes to `config/` directory. The build matrix is defined in `build.yaml` and creates artifacts for:
- `sofle_left_nice_view` - Left half with Nice View display
- `sofle_right_nice_view` - Right half with Nice View display  
- `settings_reset` - Reset device for Nice Nano v2

### Keymap Visualization
Keymap drawings are automatically generated via GitHub Actions using keymap-drawer when changes are pushed. Output SVGs are saved to `keymap-drawer/` directory.

### Local Development
To work with this codebase locally:
- Edit keymaps in `config/sofle.keymap`
- Modify physical layout in `config/sofle.json` if needed
- Update build targets in `build.yaml`
- Hardware changes require editing device tree files in `config/boards/`

### ZMK Module Dependencies
This configuration uses a custom ZMK branch with pointer/mouse support:
- Remote: `petejohanson/zmk`
- Branch: `feat/pointers-with-input-processors`
- Additional module: `GPeye/urchin-peripheral-animation` for RGB effects

## Important Notes

- The keymap includes mouse movement controls accessible through Layer 1
- RGB controls are on Layer 2 with encoder brightness adjustment
- Bluetooth pairing/clearing functions are on Layer 2  
- The configuration supports rotary encoder for volume/scroll/RGB brightness
- Home row mods use "tap-preferred" flavor with 250ms tapping term for better reliability
- always pull with rebase first before committing and pushing
- after pushing show the link to the github actions page so the user can navigate quickly