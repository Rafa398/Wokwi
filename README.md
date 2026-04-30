# Raspberry Pi Pico W Keypad-to-LED Controller

Firmware project for **Raspberry Pi Pico W (RP2040)** that reads a **4x4 matrix keypad** and drives **12 LEDs**.

> The provided source is Arduino-style C++ (`setup()`/`loop()`, `Keypad.h`) and behavior is preserved as-is.

## Features

- 4x4 keypad scanning via the `Keypad` library
- Individual LED activation for keys `1..8` and `A..D`
- Group ON/OFF controls:
  - `9`: turn ON LEDs 1..8
  - `0`: turn OFF LEDs 1..8
  - `*`: turn ON LEDs A..D
  - `#`: turn OFF LEDs A..D
- Fast polling loop (`delay(10)`) for responsive key handling

## Repository Structure

- `src/main.cpp` - Main firmware logic (unchanged behavior)
- `include/` - Reserved for headers as the project grows
- `docs/wiring.md` - Wiring and GPIO map
- `docs/architecture.md` - Firmware architecture and module notes
- `CMakeLists.txt` - Lightweight C/C++ repository scaffold

## Components (from `diagram.json`)

- 1x Raspberry Pi Pico / Pico W form-factor board
- 1x 4x4 membrane keypad
- 12x LEDs
  - 8 blue (numeric group)
  - 4 red (A/B/C/D group)
- 12x LED series resistors (220Ω)
- 4x keypad row pull-up resistors (1kΩ tied to 3V3)
- Shared GND wiring for all LED cathodes

## GPIO Mapping Summary

### Keypad

| Keypad Signal | Pico GPIO |
|---|---|
| C1 | GP19 |
| C2 | GP18 |
| C3 | GP17 |
| C4 | GP16 |
| R1 | GP26 |
| R2 | GP22 |
| R3 | GP21 |
| R4 | GP20 |

### LEDs

| LED Label | Pico GPIO |
|---|---|
| 1 | GP11 |
| 2 | GP10 |
| 3 | GP9 |
| 4 | GP8 |
| 5 | GP7 |
| 6 | GP6 |
| 7 | GP5 |
| 8 | GP4 |
| A | GP3 |
| B | GP2 |
| C | GP28 |
| D | GP27 |

See full details in [docs/wiring.md](docs/wiring.md).

## Run in Wokwi

1. Create/open a Pico project in Wokwi.
2. Use the provided `diagram.json` wiring.
3. Paste `src/main.cpp` into the firmware source (Arduino mode).
4. Ensure the `Keypad` library is available in the simulation environment.
5. Start simulation and press keypad buttons to observe LED behavior.

## Run on Real Hardware (Pico W)

### Arduino IDE (recommended for this source)

1. Install **Arduino IDE 2.x**.
2. Install board package: **Raspberry Pi Pico/RP2040**.
3. Select board: **Raspberry Pi Pico W**.
4. Install library: **Keypad** (Library Manager).
5. Open `src/main.cpp` content in a sketch and upload.
6. Wire hardware exactly as in `docs/wiring.md`.

### Pico SDK note

This source is not written in Pico SDK style (`pico/stdlib.h` etc.).
To use Pico SDK directly, a port would be required; this repository intentionally avoids logic changes.

## Wi-Fi / Credentials

- No Wi-Fi APIs are used in current firmware.
- No credentials are required or stored.
- If Wi-Fi is added later, keep credentials in a separate non-versioned config file.

## Assumptions

- Wiring and key behavior are inferred from the supplied source arrays and `diagram.json` netlist.
- LED labels in Wokwi are treated as functional names tied to GPIO mapping.
