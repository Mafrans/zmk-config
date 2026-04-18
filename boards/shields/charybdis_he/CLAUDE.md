# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Hardware Overview
Charybdis HE Left half: nRF52840 MCU (Nice!Nano v2 compatible), 29 Hall Effect keys via 4x MUX (parallel ADC scanning on P0.17/P0.20 with enables P0.09/P0.10). Shared S0/S1/S2 on P1.15/P1.13/P1.11. ZMK firmware + zmk-feature-hall-effect module.

## Build and Flash
```
west build -p -b nice_nano_v2 -- -DSHIELD=charybdis_he_left -DCONFIG_ZMK_FEATURE_HALL_EFFECT=y
west flash
```
For right half: `-DSHIELD=charybdis_he_right`.

Root `build.yaml` defines CI matrix (currently empty).

## Key Files
- `charybdis_he.dtsi`: Core device tree (kscan, transform).
- `charybdis_he-layouts.dtsi`: Physical layout (Studio).
- `*-overlay`: Left/right pin configs.
- `charybdis_he.keymap`: Behaviors.
- `charybdis_he.conf`: Kconfig options.
- `SPEC.md`: MUX wiring, sensor mapping (MUX1/3 Group1 on P0.17/P0.20 @ E=P0.09; MUX2/4 Group2 @ E=P0.10).
