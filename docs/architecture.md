# Firmware Architecture

## Overview

The firmware is a single-module Arduino-style C++ program in `src/main.cpp`.
Core behavior is event-like polling:

1. Initialize all LED GPIOs as outputs and force LOW at startup.
2. Poll keypad continuously.
3. On valid key press, dispatch action via `switch` statement.
4. Delay 10ms and repeat.

## Static Configuration

- `LEDS = 12`, `ROWS = 4`, `COLS = 4`
- `keys[4][4]`: keypad layout character map
- `ledPins[12]`: GPIO order for LED control
- `rowPins[4]`, `colPins[4]`: keypad matrix GPIO assignment

## Initialization Path

### `setup()`
- Iterates all 12 LED pins
- Sets each pin to OUTPUT
- Writes LOW to ensure all LEDs are off at reset

## Runtime Path

### `loop()`
- Calls `keypad.getKey()`
- Ignores `NO_KEY`
- For valid keys:
  - Numeric `1..8`: turn ON corresponding numeric LED
  - `9`: turn ON all numeric LEDs (indices 0..7)
  - `0`: turn OFF all numeric LEDs (indices 0..7)
  - `A..D`: turn ON corresponding alpha LED
  - `*`: turn ON all alpha LEDs (indices 8..11)
  - `#`: turn OFF all alpha LEDs (indices 8..11)
- Waits `delay(10)`

## Behavior Notes

- LEDs are latched by software state via GPIO writes.
- No debounce logic beyond loop cadence and library behavior.
- No Wi-Fi, no interrupts, no dynamic allocation.

## Extension Points (without altering current logic)

- Move pin/key mappings to a header in `include/`.
- Add optional serial diagnostics around key events.
- Add explicit “all off” key mapping if desired.
