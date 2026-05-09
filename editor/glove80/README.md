# Glove80 Layouts

MoErgo Layout Editor files for the Glove80 keyboard (80 keys, 6 rows + 6 thumb keys per side).

## Subfolders

### `tailorkey/`

Default TailorKey v5.2 bilateral macOS layout, exported unmodified from the MoErgo Layout Editor. Used as a reference template for Glove80-specific features:

- 80-key position defines (`POS_LH_C6R1` through `POS_RH_C6R6`)
- HRM `hold-trigger-key-positions` lists (includes R5/R6/T4-T6)
- `MACRO_PLACEHOLDER` macro forms
- Finger-layer R1 F-key patterns
- T4-T6 combo definitions
- `config_parameters: [{"paramName":"HID_POINTING","value":"y"}]`

### `my/`

Personal hybrid layout that maps Go60 personal key assignments onto the Glove80 hardware. See `my/README.md` for full design documentation.

## Glove80 Key Layout (80 positions)

```
R1:  10 keys (pos  0- 9)  LH_C6..C2 | RH_C2..C6
R2:  12 keys (pos 10-21)  LH_C6..C1 | RH_C1..C6
R3:  12 keys (pos 22-33)  LH_C6..C1 | RH_C1..C6
R4:  12 keys (pos 34-45)  LH_C6..C1 | RH_C1..C6
R5:  18 keys (pos 46-63)  LH_C6..C1, T1,T2,T3 | RH_T3,T2,T1, C1..C6
R6:  16 keys (pos 64-79)  LH_C6..C2, T4,T5,T6 | RH_T6,T5,T4, C2..C6
```
