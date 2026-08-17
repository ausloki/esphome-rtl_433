# esphome-rtl_433

ESPHome **decode** component for Fine Offset / Ecowitt outdoor arrays.
Consumed by [ausloki/ecowitt_systems](https://github.com/ausloki/ecowitt_systems).

## Split

| Piece | Where |
| --- | --- |
| SPI + CC1101 tuner | Stock ESPHome `cc1101:` (firmware YAML) |
| Pulse capture | Stock ESPHome `remote_receiver:` on **GDO0 only** |
| Protocol decode | This repo (`rtl_433:` component) |
| Snapshot → HA | `ecowitt_systems` (`ew_sync.h`, not this repo) |

Do **not** vendor rtl_433 C sources here or in the firmware repo. The MCU
decoder is pulled at compile time from
[juanboro/rtl_433_Decoder_ESP](https://github.com/juanboro/rtl_433_Decoder_ESP).

## Requirements

- ESP32, **ESP-IDF only** (Arduino is rejected)
- Allowlist is Fine Offset outdoor protocols only — see `reference/ALLOWLIST.md`
- Ordered CC1101 module has **no GDO2**; use GDO0-only `remote_receiver`
- YAML `frequency:` cannot retune a 433 MHz matching network

## Use from firmware

```yaml
external_components:
  - source:
      type: local
      path: ../esphome-rtl_433/components
    components: [rtl_433]
  # or: github://ausloki/esphome-rtl_433

# Do not add cc1101: / remote_receiver: until the module is wired and
# hardware_pins.md is updated in the same firmware commit.

rtl_433:
  id: rf_decode
  receiver_id: rf_receiver
  on_json_message:
    then:
      - lambda: |-
          ESP_LOGI("rtl_433", "json: %s", json::build_json([x](JsonObject root) {
            root.set(x);
          }).c_str());
```

## License

GPL-3.0 — required by rtl_433 / the MCU decoder.
