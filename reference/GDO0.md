# GDO0-only receiver

The ordered CC1101 is a 7-pin board: GND, VCC, GDO0, CSN, SCK, MOSI, MISO/GDO1.
There is **no GDO2**.

`remote_receiver:` listens on GDO0. Do not configure a second dump pin.

Pin claiming lives in `ecowitt_systems/reference/hardware_pins.md`, not here.
Do not copy candidate GPIOs into firmware until the module is Dupont'd.

VCC is 3.3 V only. Matching network is per SKU (this parcel is 433 MHz class).
