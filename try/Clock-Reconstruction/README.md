# KiCad clock/display reconstruction (draft)

## Project files

| File | Purpose |
|---|---|
| `clock_display_visual_draft.kicad_pro` | KiCad project file |
| `clock_display_visual_draft.kicad_sch` | Editable schematic sheet |
| `Clock_Reconstruction.kicad_sym` and `sym-lib-table` | Project-local custom 74260 symbol library |
| `preview/clock_display_visual_draft.svg` | KiCad-rendered preview |

Open the `.kicad_pro` file in KiCad 10.0.3; its base name matches the schematic.

## Requested changes

U18 is now a project-local custom **74260 dual 5-input NOR** symbol using the pinout in the newly supplied specifications image. Gate 1 is pins 1, 2, 3, 12, 13 to output 5; gate 2 is pins 4, 8, 9, 10, 11 to output 6; ground is pin 7 and VCC is pin 14. U18:A and its power unit are placed; the unused second gate remains available as U18:B in the custom symbol library. The schematic currently uses the DIP-14_W7.62mm footprint; select the SOIC-14 footprint instead if that matches the physical part.

Both common-anode pins (3 and 14) of each display digit now use the same local label: DS1→P1, DS2→P2, DS3→P3, and DS4→P4. The KiCad netlist verifies those nets also join U25's first four 74HC238 outputs: U25.15, U25.14, U25.13, and U25.12 respectively.

The former U1 clock symbol was replaced with Y1, a four-pin active oscillator set to 10 MHz. Its pin 3 output joins U2 pin 1 (the first counter clock input) through `CLK_10M`; pin 2 is `gnd`, and pin 4 is `vcc`. Pin 1 `EN` is tied to `vcc` under the assumed active-high enable convention. The assigned footprint is the 3.2 × 2.5 mm Abracon ASE-4Pin SMD package because no exact oscillator part number or package was specified. Confirm the selected component's enable behavior and footprint before fabrication.

## Other connectivity and remaining review

The earlier readable labels and U12-to-U15 wire are retained. KiCad's netlist confirms the shared `up`, `down`, `you`, `a/b/c`, `clr`, and `AND OUT` nets as previously documented. U18 gate-1 inputs carry the numeric labels visible in the reference (`16`, `15`, `14`, `13`, `12`), but those nets have no other confirmed endpoints in the current sheet. U18 pin 5's output destination was not clear enough to connect safely, and U18:B is not placed because only U18:A appears in the reference.

This remains a draft, not an electrically validated circuit. The counter-chain wiring, seven-segment segment/resistor-bank connections, some crossings and remaining power details still need review. The display type and polarity, resistor values/topology, and exact oscillator part are not specified. KiCad 10.0.3 successfully exported the updated schematic to SVG and netlist, but ERC has not been run because the remaining connections are incomplete. Do not fabricate or power this draft before finishing the review and running ERC.
