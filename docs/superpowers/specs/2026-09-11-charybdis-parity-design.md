# Samoklava keymap: parity with the Charybdis 3x6

## Goal

Make `config/corne.keymap` match the author's daily Charybdis layout as
closely as ZMK allows, while keeping the Samoklava-specific ZMK behaviors
that have no QMK equivalent.

## Reference

`keyboards/bastardkb/charybdis/3x6/keymaps/vendor/keymap.c` in
`mishfish/qmk_userspace` (the actively maintained custom map, QWERTY,
layers BASE / LOWER / RAISE / POINTER).

## Kept from Samoklava (not copied from QMK)

- Positional home-row mods `hml` / `hmr` with `hold-trigger-key-positions`.
- Automatic `LOWER + RAISE -> ADJUST` tri-layer.
- `&mt` / `&lt` timing tuning.
- The 4th layer stays Bluetooth + media (the Charybdis POINTER layer drives
  a trackball the Samoklava does not have).
- Outer (6th) columns stay `&none`; the board is used as an effective 36-key.

## Changes to `config/corne.keymap`

### default_layer
- Right inner thumb `&mt RCMD RET` -> `&kp RGUI` (Charybdis `PT_RCMD`).
- Right thumb `&lt RSE BSPC` -> `&lt LWR BSPC` (Charybdis `PT_BCSPC`).
- `Z` and `/` stay plain (Charybdis uses `LT(POINTER)`; author opted out).

### lower_layer
- Left row 3 (was duplicated modifiers) -> `&none &none &none &sys_reset &bootloader`
  (Charybdis `EE_CLR` / `QK_BOOT`).
- Right row 2 pinky `&kp RCTRL` -> `&kp KP_MINUS` (Charybdis `KC_PMNS`).
- Right row 3 drops the mod-tap wrappers: plain `HOME PG_DN PG_UP END`
  (also resolves the duplicated `UP` in the reference).

### raise_layer
Drops the Samoklava-only home-row mods and mod-tap symbols; plain Charybdis grid:
- Row 1 right: `^ & * [ ]`
- Row 2: `F1 F2 F3 F4 F5` | `- = < > ~`
- Row 3: `F6 F7 F8 F9 F10` | `_ + | / \`

### combos
- Add `combo_enter` on the two right thumb keys (positions `39 40`) ->
  `&kp RET` (Charybdis `lower_combo`). Every other combo already matched.

### adjust_layer
Unchanged.

## Delivery

Local branch `charybdis-parity`, committed, not pushed. Firmware build not
run locally (no ZMK toolchain); structural check of the devicetree passed
(brace balance, 12 bindings per row, 6 per thumb row).
