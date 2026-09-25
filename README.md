# PoeControl-Public

Downloads and issues for the **DMX Core PoE Control**: a PoE-powered wall
knob with push buttons that controls a DMX Core 100, a Symetrix DSP, a
Q-SYS Core, or any OSC server. Source stays private.

- Releases: https://github.com/DMXCore/PoeControl-Public/releases
- Issues: https://github.com/DMXCore/PoeControl-Public/issues
- DMX Core: https://dmxcore.com

## Downloads

One firmware image per **app** and per **board**, named
`poecontrol-<app>-<board>-<version>.uf2`. Pick the app for what the knob
talks to, and the board it is built on.

| App | Talks to | How |
|---|---|---|
| `osc` | A DMX Core 100, or any OSC server | OSC over UDP, found by mDNS |
| `symetrix` | A Symetrix DSP | its control protocol over TCP |
| `qsys` | A Q-SYS Core | the External Control Protocol over TCP |

| Board | Hardware |
|---|---|
| `w5500` | WIZnet W5500-EVB-Pico2 |
| `w6300` | Waveshare RP2350-POE-ETH |

`poecontrol-partition-table.uf2` is the same for every image and is only
needed once, for a board's first install.

## Updating

Plug the device into a PC over USB. A drive called **POECONTROL** appears.
Copy the `.uf2` for your app and board onto it. The device checks the
file, installs it, restarts into it, and goes back to the firmware it had
if the new one does not start properly. `status.txt` on the drive says how
it went. Settings are kept when the app is the same; another app's image
starts with default settings.

**First install** on a board that has never run this firmware: hold BOOTSEL
while plugging the board into USB, copy `poecontrol-partition-table.uf2`
onto the RP2350 drive that appears, and when the drive comes back, copy
the `.uf2` for your app and board.

## Configuring

The same drive holds `config.txt`. Edit it in any text editor, save, and
eject: the change applies straight away. The file explains every setting.
`status.txt` says what the device is doing and why it refused the last
edit, if it did, and `readme.txt` has the short version.

## Reporting a problem

Open an issue here. Please include:

- the `firmware` and `started` lines from `status.txt`, which name the
  image, the board and how the device last started;
- what the knob talks to (DMX Core 100, Symetrix, Q-SYS, other) and, for
  a DSP, its model;
- what you did, what you expected, and what happened - a copy of
  `status.txt` and of `config.txt` with any addresses you want kept private
  removed helps most.
