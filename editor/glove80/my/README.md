# Glove80 Hybrid Keymap (Personal)

A hybrid ZMK keymap for the MoErgo Glove80 (80 keys) that mirrors the personal Go60 layout so switching between the two keyboards is seamless.

## Goal

Create a single layout logic that works on both Glove80 and Go60. The Go60 personal layout is the **primary source** for key assignments, layer structure, and HRM timing. The Glove80 TailorKey default layout provides the **template** for 80-key structure, key position defines, and Glove80-specific features (extra rows, extra thumbs, combos for T4-T6).

## Source Files

| File | Role |
|------|------|
| `editor/go60/my/...TailorKey v4.2k macOS Bilateral - Sergey - GE lvl4.keymap` | **Primary** -- layer content, HRM timings, combos, key assignments |
| `editor/glove80/tailorkey/...TailorKey v5.2 Bilateral - macOS.keymap` | **Template** -- 80-key grid, position defines, HRM hold-trigger-key-positions, MACRO_PLACEHOLDER forms, finger-layer R1 F-key pattern, T4-T6 combos |
| `config/glove80.keymap` | **Supplement** -- parang_left/parang_right mod-morphs, T4-T6 thumb assignments, R6 edge key assignments |

## Design Decisions

### HRM System: TailorKey Bilateral

Uses the full TailorKey bilateral home-row-mod system (not the simpler `hrm_left`/`hrm_right` from `config/`). Each finger gets:
- A **primary** hold-tap (`HRM_left_index_v1B_TKZ`) for the home-row key itself
- **Cross-finger** variants (`HRM_left_index_middy`, `_ring`, `_pinky`) used on finger layers
- **Tap** macros (`HRM_left_index_tap_v1B_TKZ`) that release all mods before tapping, used on finger layers for non-home-row keys

### HRM Timing: Go60 Values (Slower)

Go60 personal timings are used instead of Glove80 TK defaults, because they were tuned for the user's typing speed:

| Finger | tapping-term | quick-tap | prior-idle |
|--------|-------------|-----------|------------|
| Index | 230 ms | 350 ms | 150 ms (L) / 80 ms (R) |
| Middle | 260 ms | 350 ms | 200 ms |
| Ring | 290 ms | 350 ms | 200 ms |
| Pinky | 320 ms | 350 ms | 200 ms |
| Thumb | 250 ms | 350 ms | 0 ms |
| Space | 250 ms | 200 ms | 0 ms |

The right index has a shorter `require-prior-idle` (80 ms vs 150 ms) to accommodate faster same-hand rolls.

### HRM Positions: Glove80 TK Values

`hold-trigger-key-positions` lists come from the Glove80 TK file because they correctly include R5/R6/T4-T6 positions (which don't exist on Go60). The `HRM_right_middy_pinky` behavior has a unique non-standard positions list.

### TailorKey Macros: Glove80 TK Forms

Macros use `MACRO_PLACEHOLDER` (Glove80 TK / newer form) instead of literal key placeholders like `A A` or `N1` (Go60 form). This applies to:
- `AS_Shifted_v1_TKZ` -- `<&kp MACRO_PLACEHOLDER>`
- `AS_v1_TKZ` -- `<&AS_HT_v2_TKZ MACRO_PLACEHOLDER MACRO_PLACEHOLDER>`
- All `_hold_` and `_tap_` macros

Exception: `mstr1_v1_TKZ` is from Go60/my (custom text output macro).

### Layer Structure: Go60 Ordering (21 Layers)

```
 0  HRM_macOS     -- Base layer with bilateral HRM
 1  Typing        -- Overlay: plain A/S/D/F, J/K/L/; and N (no HRM)
 2  Autoshift     -- All alpha/symbol keys wrapped in AS_v1_TKZ
 3  Keypad        -- Numpad on right, navigation on left
 4  Cursor        -- Text editing: select/extend word/line, arrows, clipboard
 5  Symbol        -- Programming symbols
 6  Gaming        -- WASD-centric, no HRM
 7  Mouse         -- Pointer movement, scroll, clicks
 8  MouseSlow     -- Transparent overlay, input processor scales down mouse speed
 9  MouseWarp     -- Transparent overlay, input processor scales up mouse speed (warp)
10  MouseFast     -- Transparent overlay, input processor scales up mouse speed
11  LeftIndex     -- Bilateral HRM: left index finger held
12  LeftMiddy     -- Bilateral HRM: left middle finger held
13  LeftRingy     -- Bilateral HRM: left ring finger held
14  LeftPinky     -- Bilateral HRM: left pinky finger held
15  RightIndex    -- Bilateral HRM: right index finger held
16  RightMiddy    -- Bilateral HRM: right middle finger held
17  RightRingy    -- Bilateral HRM: right ring finger held
18  RightPinky    -- Bilateral HRM: right pinky finger held
19  Magic         -- System: bootloader, BT, RGB, layer switching
20  Lower         -- Media controls, F-keys, screenshots
```

Config/'s separate Number and Function layers are dropped -- their functionality is covered by Keypad (layer 3) and combo F-keys.

## Physical Row Mapping (Go60 -> Glove80)

The Go60 has 60 keys; the Glove80 has 80. The extra 20 keys are distributed across new rows:

```
Glove80 Row   Pos Count   Go60 Equivalent         Extra Keys on Glove80
-----------   ---------   ---------------         ---------------------
R1 (func)     0-9   (10)  -- (new row)            F1-F5 / F6-F10
R2 (number)   10-21 (12)  Go60 R1                 --
R3 (QWERTY)   22-33 (12)  Go60 R2                 --
R4 (home)     34-45 (12)  Go60 R3                 --
R5 (bottom)   46-63 (18)  Go60 R4 edges + Thumbs  T1-T3 integrated into row
R6 (extra)    64-79 (16)  Go60 R5 partial + new   C5/C6 edges, T4-T6
```

## Base Layer Key Assignments

### R1 (Function Row) -- New on Glove80
Direct F1-F5 on left, F6-F10 on right. F-key combos are also kept for muscle memory with Go60.

### R2-R4 -- Same as Go60
Standard QWERTY with bilateral HRM on the home row (R4).

### R5 (Bottom + Thumbs)
- **Edges**: Same as Go60 R4 (`GRAVE Z X C V B | N M , . / td_Keypad`)
- **N key**: `&HRM_right_middy_v1B_TKZ LA(RSHFT) N` -- hold for language switch (same as Go60)
- **Thumbs T1-T3**: Same layer-tap assignments as Go60:
  - Left: T1=Cursor/BSPC, T2=Keypad/DEL, T3=Lower/ESC
  - Right: T3=CAPS, T2=Mouse/RET, T1=Symbol/SPACE

### R6 (Extra Bottom + T4-T6)
- **LH edges**: `magic parang_left LBKT RBKT parang_right`
  - `parang_left`/`parang_right`: mod-morph from `config/` -- `(` or `<` with shift / `)` or `>` with shift
- **T4-T6** (from `config/`, plain `&kp` since T1-T3 already have layer-taps):
  - Left: T4=BSPC, T5=DEL, T6=LG(S)
  - Right: T6=BSPC, T5=ENTER, T4=SPACE
- **RH edges**: `LEFT DOWN UP RIGHT PG_DN` (arrow cluster from `config/`)

## Combos

### From Go60/my (kept for muscle memory)
- **F1-F10**: Adjacent R1+R2 key pairs (e.g., C5R1+C5R2 for F1)
- **F5/F6**: Adapted positions since `POS_LH_C1R1` doesn't exist on Glove80 -- uses `C2R1+C1R2` instead
- **F11**: RH C6R1+C6R2
- **F12**: RH C6R1+C5R1
- **Sticky Hyper/Meh**: RH C2R4+C2R5 / C3R5+C3R4
- **Gaming toggle**: LH C2R5+C1R4
- **Capslock**: Both T1 keys
- **Alt-Tab**: LH T1+C1R4 (GUI+Tab in Cursor layer)
- **Ctrl-Tab**: LH C2R5+C2R4

### From Glove80 TK (T4-T6 specific)
- **Caps Lock**: LH T6+T2 or RH T2+T6
- **Caps Word**: LH T5+T4 or RH T5+T4
- **Alt-Tab**: LH T3+T6
- **Ctrl-Tab**: LH T2+T5
- **Win-Tab**: LH T1+T4
- **Meh (right)**: RH T2+T5
- **Gaming toggle**: LH C1R5+C2R6

## Omitted (Go60-specific hardware)

- Cirque trackpad input listeners (`zip_click_to_right_click_mapper`)
- Go60-specific key positions (`POS_LH_C1R1`, `POS_RH_C1R1` -- these columns don't exist on Glove80)
