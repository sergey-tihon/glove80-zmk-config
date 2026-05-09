# Go60 Layouts

MoErgo Layout Editor files for the Go60 keyboard (60 keys, 5 rows + 3 thumb keys per side).

## Subfolders

### `tailorkey/`

Default TailorKey v4.2m bilateral macOS layout, exported unmodified from the MoErgo Layout Editor. Used as a reference for the default TailorKey configuration on Go60.

### `my/`

Personal layout -- the primary source of truth for key assignments, layer structure, HRM timings, and combos. This layout was tuned over time and drives the Glove80 hybrid layout (`editor/glove80/my/`).

Key characteristics:
- TailorKey bilateral HRM system with custom (slower) timings
- 21 layers: HRM_macOS, Typing, Autoshift, Keypad, Cursor, Symbol, Gaming, Mouse, MouseSlow, MouseWarp, MouseFast, 8 finger layers, Magic, Lower
- N key with `LA(RSHFT)` hold for language switching
- Cirque trackpad input listeners (Go60-specific hardware)

## Go60 Key Layout (60 positions)

```
R1:  12 keys (pos  0-11)  LH_C6..C1 | RH_C1..C6
R2:  12 keys (pos 12-23)  LH_C6..C1 | RH_C1..C6
R3:  12 keys (pos 24-35)  LH_C6..C1 | RH_C1..C6
R4:  12 keys (pos 36-47)  LH_C6..C1 | RH_C1..C6
R5:  12 keys (pos 48-59)  LH_C4..C2, T1,T2,T3 | RH_T3,T2,T1, C2..C4
```
