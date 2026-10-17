# Mono Keyboard

This is an archive repository for Mono 65% keyboard.

It should include everything that you need to manufacture one yourself.

## Building QMK

First, download/clone [QMK source](https://github.com/qmk/qmk_firmware) and copy the `mono` from this repository into QMK's `keyboards` directory.

There, run `$ make mono:default` which will build a `mono_default.hex` file that you can then flash onto the board.

## VIA

`qmk/mono/via.json` is the VIA V3 definition. Until it is merged into VIA's
keyboard repository, load it manually: in [usevia.app](https://usevia.app) open
Settings, enable "Show Design tab", then in the Design tab click "Load" and pick
the file. Layout options (split backspace, ISO/ANSI Enter, ISO/ANSI left Shift)
are in the Configure tab under "Layouts".

The PCB is wired for ISO: the ANSI Enter shares a matrix position with ISO `#`
(`[2,12]`) and the ANSI backslash shares one with ISO Enter (`[2,13]`). Choosing
the ANSI Enter layout in VIA only changes the drawing, so on an ANSI build also
remap Enter (`[2,12]`) to `KC_ENT` and backslash (`[2,13]`) to `KC_BSLS`.
