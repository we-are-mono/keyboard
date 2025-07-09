# Mono Keyboard

This is an archive repository for Mono 65% keyboard.

It should include everything that you need to manufacture one yourself.

## Building QMK

First, download/clone [QMK source](https://github.com/qmk/qmk_firmware) and copy the `mono` from this repository into QMK's `keyboards` directory.

There, run `$ make mono:default` which will build a `mono_default.hex` file that you can then flash onto the board.
