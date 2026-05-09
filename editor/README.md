# Editor Layouts

MoErgo Layout Editor export files for both keyboards. Each subfolder contains `.keymap` (ZMK devicetree) and `.json` (editor metadata) file pairs.

## Structure

```
editor/
  glove80/           # MoErgo Glove80 (80 keys)
    tailorkey/       #   Default TailorKey v5.2 bilateral macOS layout
    my/              #   Personal hybrid layout (Go60 logic on Glove80 hardware)
  go60/              # MoErgo Go60 (60 keys)
    tailorkey/       #   Default TailorKey v4.2m bilateral macOS layout
    my/              #   Personal layout (primary source of truth)
```

## Naming Convention

Files exported from the MoErgo Layout Editor use the format:

```
<uuid>_<layout title>.keymap
<uuid>_<layout title>.json
```

The `my/` folders for Glove80 use simplified names (`glove80.keymap`, `glove80.json`) since they are generated/maintained locally rather than exported directly from the editor.

## Relationship Between Layouts

The **Go60 personal layout** (`go60/my/`) is the primary source of truth for key assignments, layer structure, HRM timings, and combos. The **Glove80 personal layout** (`glove80/my/`) is a hybrid that maps Go60 logic onto the 80-key Glove80 hardware, adding:

- R1 function row (F1-F10)
- Extra thumb keys T4-T6
- R6 edge keys (parang mod-morphs, arrows)
- Glove80-specific combos for the additional keys

The `tailorkey/` folders contain unmodified reference copies of the default TailorKey bilateral macOS layouts for each keyboard.
