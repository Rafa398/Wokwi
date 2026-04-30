# Wiring Reference (Raspberry Pi Pico W)

This document maps the supplied Wokwi `diagram.json` connections to Pico W GPIO usage.

## 1) Keypad Connections (4x4 matrix)

### Columns
- C1 -> GP19
- C2 -> GP18
- C3 -> GP17
- C4 -> GP16

### Rows
- R1 -> GP26
- R2 -> GP22
- R3 -> GP21
- R4 -> GP20

### Pull-up network
Each row is also connected through a 1k resistor to 3V3:
- R1 via `rp1` (1k)
- R2 via `rp2` (1k)
- R3 via `rp4` (1k)
- R4 via `rp3` (1k)

## 2) LED Connections

All LED cathodes (C) are tied to Pico GND.
Each LED anode (A) is connected to a GPIO through a 220Ω resistor.

| LED | GPIO | Resistor |
|---|---|---|
| 1 | GP11 | r8 (220Ω) |
| 2 | GP10 | r7 (220Ω) |
| 3 | GP9 | r6 (220Ω) |
| 4 | GP8 | r5 (220Ω) |
| 5 | GP7 | r4 (220Ω) |
| 6 | GP6 | r3 (220Ω) |
| 7 | GP5 | r2 (220Ω) |
| 8 | GP4 | r1 (220Ω) |
| A | GP3 | r9 (220Ω) |
| B | GP2 | r10 (220Ω) |
| C | GP28 | r11 (220Ω) |
| D | GP27 | r12 (220Ω) |

## 3) UART in Wokwi

- GP0 -> Serial monitor RX
- GP1 -> Serial monitor TX

No serial output is used in the current firmware, but wiring exists in the diagram.

## 4) Practical Hardware Notes

- Keep a common ground between Pico W and all LED/keypad circuits.
- 220Ω LED resistors are safe for indicator brightness/current limiting.
- The 1k pull-ups on keypad rows are present in the original design and preserved here.
