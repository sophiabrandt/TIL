# Flash Keyboard With QMK

I have a [3w6](https://github.com/weteor/3W6), an ortholinear split keyboard with a QMK firmware.\
Mine is a prebuilt version from [Keebart](https://www.keebart.com/de/produkte/3w6).

Keebart maintains a [QMK fork](https://github.com/Keebart/vial-qmk-3w6-rgb) of the original.

Here are the steps to install and flash the firmware onto the 3w6.

## Install QMK

See [docs.qmk.fm](https://docs.qmk.fm/).

```bash
brew install qmk/qmk/qmk
```

## Clone repository

```bash
git clone https://github.com/Keebart/vial-qmk-3w6-rgb.git
cd vial-qmk-3w6-rgb
```

## Setup QMK

```bash
qmk setup
```

## Build Keymap

```bash
make keebart/3w6_rgb:vial
```

```bash
qmk compile -kb ferris/sweep -km vial -e CONVERT_TO=rp2040_ce
```

## Flash Keymap

- Disconnect the keyboard from the computer.
- Press the "Q" button, which is the top-left button on the left side of the keyboard directly below the USB connector.
- While holding down the "Q" button, connect the keyboard back to the computer.

```bash
qmk flash -kb keebart/3w6_rgb -km vial
```
