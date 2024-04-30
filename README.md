# USB CAN Adapter

An STM32F0 USB CAN interface. I couldn't find a decent option in stock, so built this. It works,
but is not well documented and should be considered a project not a product ;).

![3D rendering of USB CAN board](/docs/3d_render.png?raw=true "USB CAN Render")

## Rev 1 Errata

- The BOOT0 button is backwards. It should be grounded by default and pulled high by the button.
- The jumper holes are too small for most 0.1" headers and need to be enlarged.
