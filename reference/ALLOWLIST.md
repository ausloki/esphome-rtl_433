# Protocol allowlist

This repo is consumed by [ausloki/ecowitt_systems](https://github.com/ausloki/ecowitt_systems).
That bench's outdoor array is **Ecowitt WS69** (confirmed 2026-08-17).

Compiled in via `-DMY_RTL433_DEVICES=...` so the S3 does not carry the full
rtl_433 device table.

| DECL | rtl_433 model | Why |
| --- | --- | --- |
| `fineoffset_WH25` | Fineoffset-WH24 / Fineoffset-WH65B | Truncated WS69 packets may appear as WH65B |
| `fineoffset_wh1080` | Fineoffset-WHx080 | Related Fine Offset 5-in-1 OOK |
| `fineoffset_wh1080_fsk` | Fineoffset-WHx080 | FSK variant |

## Not in this snapshot

**Fineoffset-WS69** (merbanan/rtl_433 #3426, Dec 2025) is **not** in
juanboro/rtl_433_Decoder_ESP yet. Full 260-bit WS69 frames will be rejected
until we port that decoder. Truncated packets may still decode as WH65B.

Do **not** add WH31 / WH51 / soil extras — WS2320 does not pair them, and
they would spend RAM on neighbour traffic.

Indoor T/H/P never appear on this RF path. Those come from WS2320 HTTP listen.
