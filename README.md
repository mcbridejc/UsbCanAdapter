# USB CAN Adapter

An STM32F0 USB CAN interface. I couldn't find a decent option in stock, so built this. It works,
but is not well documented and should be considered a project not a product ;).

![3D rendering of USB CAN board](/docs/3d_render.png?raw=true "USB CAN Render")

## Firmware

This board can use the "cantact" firmware from https://github.com/candle-usb/candleLight_fw. In the
release archive, the file is "cantact_fw.bin". It is also included in the repo here for reference.

It can be programmed via the built-in DFU bootloader. To get into boot loader, pull boot0 high while
powering on, using the BOOT0 button (See rev1 errata; some bodge wires are required for this).

On linux, you can use `dfu-util`, like so:

```
dfu-util -D cantact_fw.bin -d 0483:df11 -a 0 -s 0x08000000
```

ST has a DFU programming tool for windows (and there are others)

## Jumpers

There are three shortable jumpers:

- "TERM" connects a 120 ohm termination resistor between CAN_H and CAN_L.
- "POWER_ISO" (two jumpers) connect the USB 5V and ground to the isolated CAN bus side of the
  transceiver. If these are left unconnected, the CAN bus is electrically isolated from the MCU/USB
  side of the board, but 5V must be provided from elsewhere.

## Reminders for using on linux

`sudo ip link set can0 type can bitrate 1000000`
`sudo ip link set up can0 txqueuelen 1024`

For a GUI, SavvyCAN works. Create the connection as a "QT SerialBus" device, with devicetype "socketcan". It seems the link must be manually brought up and bitrate set on the command line first; savvy can isn't going it (maybe because of permissions?).


## Rev 1 Errata

- The BOOT0 button is backwards. It should be grounded by default and pulled high by the button.
- The jumper holes are too small for most 0.1" headers and need to be enlarged.
