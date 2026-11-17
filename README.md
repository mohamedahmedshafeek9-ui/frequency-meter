# Frequency Meter (Discrete-IC Design)

> A 4-digit digital frequency counter built entirely from logic ICs (no microcontroller, no firmware), designed in **KiCad** and simulated in **Proteus**. A Schmitt-trigger input stage conditions the signal, a 10 MHz oscillator generates the gate times with **auto-ranging**, decade counters count pulses during the gate, and 4511 latch/decoder/drivers show the result with the correct **decimal point** on four 7-segment displays. Tested from **1 Hz to 10 MHz**.

![Status](https://img.shields.io/badge/status-tested%2C%20PCB%20in%20progress-brightgreen) ![KiCad](https://img.shields.io/badge/design-KiCad-blue) ![Proteus](https://img.shields.io/badge/simulation-Proteus-purple) ![Logic](https://img.shields.io/badge/logic-74xx%20%2F%204xxx-orange) ![License](https://img.shields.io/badge/license-CU-lightgrey)

## Overview

The meter uses **direct (gated) counting**: `f = N / T_gate`. A 10 MHz timebase is divided down through cascaded decade counters to produce accurate gate intervals. While the gate is open, input pulses are counted by BCD decade counters; at gate close the count is latched into the display decoders and the counters are cleared for the next cycle.

| Gate time | Resolution | Full-scale (4 digits, 9999 counts) |
|---|---|---|
| 1 s | 1 Hz | 9.999 kHz |
| 0.1 s | 10 Hz | 99.99 kHz |
| 10 ms | 100 Hz | 999.9 kHz |
| 1 ms | 1 kHz | 9.999 MHz |

<!-- EDIT: keep only the gate times your design actually offers; full-scale = 9999 / T_gate -->

## Features

- Pure digital-logic design: **26 ICs**, no microcontroller or firmware
- Crystal-based timebase: **10 MHz active oscillator** (accuracy set by oscillator tolerance, ±1 count)
- **4-digit** 7-segment readout (KCSC02-105), latched, flicker-free
- **Auto-ranging:** gate time switches automatically to keep the reading in range
- **Automatic decimal point** placement for the selected range
- **Schmitt-trigger input stage:** clean edges from slow, noisy or sine inputs <!-- EDIT: implementation (IC / discrete) -->
- **Tested from 1 Hz to 10 MHz**
- On-board **5 V** regulation (L7805)
- Full KiCad project (schematic, DIP footprints, netlist-verified inventory) plus a **Proteus** schematic / simulation
- **PCB layout in progress**

## Bill of Materials (ICs)

Quantities are from the validated KiCad netlist (see [`docs/IC_Inventory.xlsx`](docs/IC_Inventory.xlsx)).

| IC | Qty | Refs | Package | Function |
|---|---|---|---|---|
| 74HC390 | 7 | U2, U3, U4, U8, U10, U11, U17 | DIP-16 | Dual decade counter (timebase divider chain + pulse counting) |
| 4511 | 4 | U9, U14, U16, U23 | DIP-16 | BCD → 7-segment latch / decoder / driver, one per digit |
| 74LS08 | 4 | U7, U12, U13, U21 | DIP-14 | Quad 2-input AND (gating / control logic) |
| 74HC74 | 3 | U6, U19, U20 | DIP-14 | Dual D flip-flop (gate / control sequencing) |
| 74LS04 | 3 | U15, U26, U27 | DIP-14 | Hex inverter |
| 74HC151 | 1 | U5 | DIP-16 | 8-to-1 multiplexer |
| 74HC238 | 1 | U25 | DIP-16 | 3-to-8 decoder / demultiplexer |
| 74LS193 | 1 | U22 | DIP-16 | Synchronous 4-bit up/down counter |
| 74260 | 1 | U18 | DIP-14 | Dual 5-input NOR (custom KiCad symbol: gate 1 pins 1,2,3,12,13 → 5; gate 2 pins 4,8,9,10,11 → 6; GND 7, VCC 14) |
| L7805CV | 1 | U28 | TO-220 | 5 V linear regulator |
| **Total** | **26** | | | |

**Non-IC parts:** 4 × KCSC02-105 7-segment displays (U24, U29, U30, U31); 1 × 10 MHz 4-pin active oscillator Y1 (SMD, 3.2 × 2.5 mm).

<!-- EDIT: confirm the role of U5 (74HC151), U25 (74HC238), U22 (74LS193) in your schematic, e.g. "U5 selects the gate time", "U25 drives decimal point / range LEDs" -->

### Part-family notes

Some schematic Value fields differ from the KiCad library symbol; confirm the exact family before buying parts or fabricating a PCB:

- **74390:** library symbol is 74LS390, schematic value says 74HC390 (all 7 ICs).
- **74151:** library symbol 74LS151, schematic value 74HC151.
- **7408 / 74LS08:** values read `7408`, `AND` or `AND gate`; library part is 74LS08.
- **7474:** U19 and U20 are labelled `7474` but use the 74HC74 symbol (U6 is `74HC74`).
- **Inverters:** U15, U26, U27 are labelled generic `NOT`; library part is 74LS04.
- **4511:** no family/manufacturer suffix (CD4511 / MC14511 / 74HC4511).
- **Mixed LS / HC / CMOS 4000-series** at 5 V: check input thresholds and drive levels where LS outputs feed HC/CMOS inputs.
- **L7805CV:** confirm input voltage, load current and heatsinking (TO-220).

## Circuit Description

1. **Input conditioning:** a Schmitt-trigger stage squares up the input into clean logic-level edges (hysteresis rejects noise and slow edges).
2. **Timebase:** Y1 (10 MHz) feeds a chain of 74HC390 decade counters that divide it down to the gate frequencies.
3. **Auto-range & decimal point:** control logic (mux, decoder, flip-flops, gates) picks the gate time that keeps the count in range and drives the matching decimal point. <!-- EDIT: describe how overrange / underrange is detected and which ICs do it -->
4. **Counting:** with the gate open, input pulses ripple through cascaded BCD decade counters.
5. **Latch & display:** at gate close, the count is latched into the four 4511 drivers (internal latch) and shown on the 7-segment displays.
6. **Reset:** counters are cleared before the next gate opens.
7. **Power:** L7805CV regulates the supply to 5 V for all logic.

## Repository Structure

```
frequency-meter/
├── <project>.kicad_pro      # KiCad project
├── <project>.kicad_sch      # Schematic
├── <project>.kicad_pcb      # PCB layout (if any)
├── libs/                    # Custom symbols (e.g. Clock_Reconstruction:74260)
├── proteus/
│   └── <project>.pdsprj     # Proteus schematic / simulation
├── docs/
│   ├── IC_Inventory.xlsx    # Netlist-verified IC inventory
│   └── schematic.pdf
└── README.md
```
<!-- EDIT: match your real folder layout -->

## Getting Started

### KiCad (schematic / PCB)

1. Install [KiCad](https://www.kicad.org/). <!-- EDIT: version -->
2. Clone the repo and open the `.kicad_pro` file:
   ```bash
   git clone https://github.com/mohamedahmedshafeek9-ui/frequency-meter.git
   ```
3. If KiCad reports a missing 74260 symbol, add the custom `Clock_Reconstruction` symbol library.

### Proteus (simulation)

1. Open `proteus/<project>.pdsprj` in Proteus. <!-- EDIT: filename / version -->
2. Set the input generator to the test frequency (1 Hz – 10 MHz) and run the simulation.
3. Read the value and decimal point on the four 7-segment displays.

### Building the hardware

1. Power the circuit from a DC supply suitable for the L7805CV (typically 7–12 V in, 5 V out).
2. Connect the signal source to the input with **common ground**. Logic inputs tolerate only **0 V to V_CC**; use a series resistor with clamp diodes for anything beyond that.
3. Decouple every IC with a **100 nF** capacitor close to its supply pins.

## Design Notes

- **Range limit:** the 4-digit display holds 9999 counts; auto-ranging shortens the gate as the input frequency rises.
- **±1 count error:** inherent to gated counting, worst at low frequencies; a longer gate reduces the relative error.
- **Maximum input frequency** is limited by the slowest counter in the input path (74LS ≈ 25–30 MHz, 74HC ≈ tens of MHz at 5 V).

## Results / Testing

Tested across **1 Hz to 10 MHz** against a function generator. <!-- EDIT: name your reference instrument -->

| Applied frequency | Displayed | Error |
|---|---|---|
| 1 Hz | <...> | <...> |
| 10 Hz | <...> | <...> |
| 100 Hz | <...> | <...> |
| 1 kHz | <...> | <...> |
| 10 kHz | <...> | <...> |
| 100 kHz | <...> | <...> |
| 1 MHz | <...> | <...> |
| 10 MHz | <...> | <...> |

<!-- EDIT: fill in measured values -->

## Roadmap

- [x] Auto-ranging, automatic decimal point, Schmitt-trigger input
- [x] Verified from 1 Hz to 10 MHz
- [ ] PCB layout and fabrication (in progress)

## License



## Author

**Mohamed Ahmed Shafeek** — [@mohamedahmedshafeek9-ui](https://github.com/mohamedahmedshafeek9-ui)
Faculty of Engineering, Cairo University — Electronics & Electrical Communications
