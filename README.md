# QMK Keymaps for Dactyl Manuform

This repository contains QMK keymap configurations for **Dactyl Manuform** keyboards, optimized for GitHub Actions automated building.

## 🎯 Available Templates

### 1. **Full Bilateral Layout** (`dactyl-manuform-5x6.json`)
- **Type**: Complete left + right side layout
- **Use Case**: Standard typing with full QWERTY
- **Layers**: 3 layers (base, symbols/numbers, function keys)
- **Target**: `handwired/dactyl_manuform/5x6`

### 2. **Right Side Only Template** (`almang45.json`)
- **Type**: Clean right-side only template
- **Use Case**: Professional numpad with navigation and function keys
- **Layers**: 2 layers (numpad + functions)
- **Target**: `handwired/dactyl_manuform/5x6`

### 3. **Matrix Layout Definition** (`almang45-first-matrix.json`)
- **Type**: Matrix-based layout definition
- **Use Case**: Custom layout configuration for right side
- **Layers**: 1 layer (custom matrix)
- **Target**: `handwired/dactyl_manuform/5x6`

## 🚀 Usage

### GitHub Actions Build
Push any changes to automatically build all configured keymaps:

```yaml
# Configured keymaps will be built automatically
- almang45-first-matrix.json
- dactyl-manuform-5x6.json
- almang45.json
```

### Local Build
If you have QMK CLI installed:

```bash
# Build any template
qmk compile almang45-first-matrix.json
qmk compile dactyl-manuform-5x6.json
qmk compile almang45.json

# Convert to keymap.c
qmk json2c dactyl-manuform-5x6.json
```

## 📋 Layout Details

### Right Side Only Template Layout (`almang45.json`)

#### Layer 0 (Base - Numpad)
```
[ ][ ][ ][ ][ ][ ]
[NL][/][*][-][BS][DEL]
[ ][ ][ ][ ][ ][ ]
[7][8][9][+][HM][PU]
[ ][ ][ ][ ][ ][ ]
[4][5][6][+][END][PD]
[ ][ ][ ][ ][ ][ ]
[1][2][3][V-][V+][INS]
[ ][ ][0][ENT][ ][ ]
[ENT][L1][ ][ ][ ][ ]
[ ][ ][ ][ ][ ][ ]
[L1][SP][→][ ]
```

#### Layer 1 (Functions)
```
[ ][ ][ ][ ][ ][ ]
[F1][F2][F3][F4][F5][F6]
[ ][ ][ ][ ][ ][ ]
[F7][F8][F9][F10][F11][F12]
[ ][ ][ ][ ][ ][ ]
[MU][V-][V+][PL][PR][NX]
[ ][ ][ ][ ][ ][ ]
[CP][SL][PS][PR][IN][DEL]
[ ][ ][CT][AL][ ][ ]
[TAB][--][ ][ ][ ][ ]
[ ][ ][ ][ ][ ][ ]
[--][ENT][BS][ ]
```

**Legend:**
- `NL` = Num Lock, `V-` = Vol Down, `V+` = Vol Up
- `L1` = Layer 1 (hold), `--` = Transparent/Pass-through
- `MU` = Mute, `PL` = Play, `PR` = Previous, `NX` = Next
- `CP` = Caps Lock, `SL` = Scroll Lock, `PS` = Print Screen
- `CT` = Ctrl, `AL` = Alt, `SP` = Space, `→` = Right Arrow

## 🔧 Customization

1. **Edit existing templates** - Modify the JSON files directly
2. **Create new templates** - Copy and modify any existing template
3. **Add to workflow** - Update `.github/workflows/build.yml` to include new files
4. **Test locally** - Use QMK CLI to test before pushing

## 🎮 Hardware Configuration

All templates are configured for:
- **Keyboard**: `handwired/dactyl_manuform/5x6`
- **Layout**: `LAYOUT_5x6`
- **Wiring**: Standard Dactyl Manuform wiring

## 📚 Resources

- [QMK Configurator](https://config.qmk.fm) - Visual keymap editor
- [QMK Documentation](https://docs.qmk.fm) - Complete QMK guide
- [Dactyl Manuform Build Guide](https://github.com/abstracthat/dactyl-manuform) - Hardware assembly

## 🔄 Workflow

1. **Modify** keymap JSON files
2. **Push** to trigger GitHub Actions
3. **Download** built firmware from Actions artifacts
4. **Flash** to your keyboard

Built firmware files will be available as GitHub Actions artifacts in `.hex`, `.bin`, and `.uf2` formats.
