# Mono Keyboard

This is an archive repository for Mono 65% keyboard.

It should include everything that you need to manufacture one yourself.

## Building QMK

First, download/clone [QMK source](https://github.com/qmk/qmk_firmware) and copy the `mono` from this repository into QMK's `keyboards` directory.

There, run `$ make mono:default` which will build a `mono_default.hex` file that you can then flash onto the board.

## Remapping keys with VIA

Keys are remapped live with [VIA](https://usevia.app); changes are stored on the
keyboard and need no reflashing. The `default` keymap already has VIA enabled.

`qmk/mono/via.json` is the VIA V3 definition. Until it is merged into VIA's
keyboard repository, VIA needs it loaded once (step 3).

1. Use a Chromium-based browser (Chrome, Edge, Brave). Firefox and Safari have
   no WebHID support.
2. On Linux, allow your user to access the keyboard, then replug it:

   ```
   echo 'KERNEL=="hidraw*", SUBSYSTEM=="hidraw", ATTRS{idVendor}=="4d4f", ATTRS{idProduct}=="4e4f", MODE="0660", TAG+="uaccess"' | sudo tee /etc/udev/rules.d/99-mono.rules
   sudo udevadm control --reload-rules
   ```

3. Open [usevia.app](https://usevia.app), go to Settings and enable "Show
   Design tab". In the Design tab click "Load" and pick `qmk/mono/via.json`.
   The browser remembers it, so this is needed only once.
4. Click "Authorize device" and pick "Mono".
5. In the Configure tab, under "Layouts", pick the options that match your
   build (split backspace, ISO/ANSI Enter, ISO/ANSI left Shift). This only
   changes the drawing, not what the keys send.
6. Under "Keymap", pick the layer at the top (0 to 3), click a key on the
   drawing, then click the keycode it should send in the panel below. It is
   saved immediately.
7. Test in the "Key Tester" tab: pressed keys light up.

Tips:

- Layer 0 is the base layer. Layer 1 is held with Fn (`MO(1)`, right of
  right Alt) and has F1 to F12 on the number row and backlight step on `B`.
  Layers 2 and 3 are empty.
- `▽` (`KC_TRNS`) falls through to the layer below. Layer keys (`MO`, `TG`,
  `LT`, ...) are in the "Layers" group; any QMK keycode can be typed in via
  "Special" → "Any".
- Macros are recorded in the "Macros" tab and assigned like any other key.
- "Save + Load" exports the whole keymap to a file and restores it.
- Holding Esc while plugging the keyboard in starts the bootloader for
  flashing and also resets the keymap to the defaults above.

### ANSI Enter

The PCB is wired for ISO: the ANSI Enter shares a matrix position with ISO `#`
(`[2,12]`) and the ANSI backslash shares one with ISO Enter (`[2,13]`). With
ANSI keycaps, swap the `|` and Enter keys: set `[2,12]` to `KC_ENT` and `[2,13]`
to `KC_BSLS`. Choosing the ANSI Enter layout in VIA only changes the drawing;
the swap is what makes the keys work.

Where the drawing is ISO (QMK Configurator, or VIA with Layouts left on ISO)
this looks odd: Enter shows on the small `#` key and `|` on the tall ISO Enter.
It still works correctly on the keyboard.
