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

## Configuring

There are two ways in, and they edit the same file.

**The drive.** Plug the device into a PC over USB. A drive called
**POECONTROL** appears, holding `config.txt`. Edit it in any text editor,
save, and eject: the change applies straight away. The file explains every
setting. `status.txt` says what the device is doing and why it refused the
last edit, if it did, and `readme.txt` has the short version.

**The web page.** Once the device is on the network, open
`http://<name>.local/` in a browser - `http://poecontrol-<id>.local/` until
it is given a name; `status.txt` on the drive prints the exact address, and
a plain `http://<ip address>/` works too. The page shows the same status
live, has `config.txt` in an editor with a Save button that applies the
change the same way the drive does, lists the servers or controls the
device can see, shows its log, takes a firmware `.uf2` upload, and can
restart it. Nothing on the wall needs touching.

**Password.** The page has none until one is set on it, and says so.
With a password set, the page asks for it before anything can be changed;
the status stays visible. A forgotten password is removed from the drive:
add the line `password = none` to `config.txt`.

**Off altogether.** A device that must not be reachable over the network
at all gets `web = off` in `config.txt`. It then listens on no TCP port,
and the drive is the only way to change or update it. The setting takes
effect at the next restart; `status.txt` says which state is in force.

## Updating

**From the web page:** choose the `.uf2` for your app and board under
Firmware, and upload it.

**From the drive:** copy the `.uf2` for your app and board onto the
**POECONTROL** drive.

Either way the device checks the file, installs it, restarts into it, and
goes back to the firmware it had if the new one does not start properly.
`status.txt` and the page say how it went. Settings are kept when the app
is the same; another app's image starts with default settings.

**First install** on a board that has never run this firmware: hold BOOTSEL
while plugging the board into USB, copy `poecontrol-partition-table.uf2`
onto the RP2350 drive that appears, and when the drive comes back, copy
the `.uf2` for your app and board.

## Reporting a problem

Open an issue here. Please include:

- the `firmware` and `started` lines from `status.txt` or the page's
  status, which name the image, the board and how the device last started;
- what the knob talks to (DMX Core 100, Symetrix, Q-SYS, other) and, for
  a DSP, its model;
- what you did, what you expected, and what happened - a copy of
  `status.txt` and of `config.txt` with any addresses you want kept private
  removed helps most, and the page's log if the device is on the network.
