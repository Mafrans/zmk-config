### Hardware Spec Summary

**MCU:** nRF52840 (SuperMini NRF52840, Nice!Nano v2.0 pin-compatible)  
**Firmware:** ZMK + `zmk-feature-hall-effect` module  
**Switches:** Raed's HE (Linear Hall Effect)  
**Layout:** Left half, **29 keys** (4x8 mux matrix = 32 channels, 3 unused)  
**Scanning:** Parallel multiplexed ADC (2x speed via shared enables/Z lines)  

#### MUX Wiring (Verified by Multimeter)
| MUX | S0 (shared) | S1 (shared) | S2 (shared) | Z (ADC) | E (Enable) | Group |
|-----|-------------|-------------|-------------|---------|------------|-------|
| **MUX1** | P1.15 | P1.13 | P1.11 | **P0.17** | **P0.09** | Group 1 (w/ MUX3) |
| **MUX2** | P1.15 | P1.13 | P1.11 | **P0.17** | **P0.10** | Group 2 (w/ MUX4) |
| **MUX3** | P1.15 | P1.13 | P1.11 | **P0.20** | **P0.09** | Group 1 (w/ MUX1) |
| **MUX4** | P1.15 | P1.13 | P1.11 | **P0.20** | **P0.10** | Group 2 (w/ MUX2) |

**Parallel Read Logic:**
- **E=P0.09 HIGH:** MUX1 (P0.17) + MUX3 (P0.20) read simultaneously
- **E=P0.10 HIGH:** MUX2 (P0.17) + MUX4 (P0.20) read simultaneously

**Sensor Mapping Assumption (for keymap):**
- MUX1 Ch0-7 → Keys 0-7 (Row 1)
- MUX2 Ch0-7 → Keys 8-15 (Row 2)
- MUX3 Ch0-7 → Keys 16-23 (Row 3)
- MUX4 Ch0-4 → Keys 24-28 (Thumb cluster; Ch5-7 unused)

This matches your multimeter results (Steps 1-4 PASS). **Ready for build fix or calibration?** Reply "BUILD" or "CALIBRATE".
