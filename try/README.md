# Multiplexed clock/display controller — KiCad reconstruction

## Open the project

Open `clock_display_visual_draft.kicad_pro` in KiCad 10. The project includes the editable schematic, the custom 74260 symbol, project-local library tables, and a rendered schematic preview.

| File | Purpose |
|---|---|
| `clock_display_visual_draft.kicad_pro` | KiCad project |
| `clock_display_visual_draft.kicad_sch` | Editable schematic |
| `Clock_Reconstruction.kicad_sym` | Custom dual five-input NOR symbol for U18 |
| `sym-lib-table`, `fp-lib-table` | Project-local symbol and footprint library mappings |
| `preview/Clock_Reconstruction.pdf` | Full-page schematic preview |
| `preview/Clock_Reconstruction.svg` | Zoomable vector schematic preview |
| `preview/Clock_Reconstruction.png` | Raster page thumbnail |
| `validation/ERC_summary.md` | Final ERC result and remaining warnings |
| `validation/netlist.xml` | KiCad-exported connectivity netlist |

The footprint table uses KiCad 10's `${KICAD10_FOOTPRINT_DIR}` variable. If KiCad reports a missing library on another machine, configure the standard KiCad 10 footprint library table or point this variable at that installation's footprints.

## Implemented wiring

- **U18 custom 74260:** Gate 1 inputs 1, 2, 3, 12, 13 feed output 5; gate 2 inputs 4, 8, 9, 10, 11 feed output 6; pins 7 and 14 are GND and VCC. Gate 1 output pin 5 drives U21; U21 and U26 route the control to U22 DOWN. U18's unused second-gate inputs are grounded and its output is marked no-connect.
- **Timebase:** Y1 is represented as a four-pin active 10 MHz oscillator. Pins 1/4 are VCC, pin 2 is GND, and pin 3 is `CLK_10M`. The current footprint is a 3.2 × 2.5 mm Abracon ASE-style SMD oscillator; confirm the selected physical part, enable pin behavior, and package before assembly.
- **Diode matrix:** Fourteen 1N4007 symbols are arranged as in the PDF, with P outputs on diode anodes and the grouped mode/frequency signals on cathodes: P4/P7→K1; P3/P6→K100; P2/P5/P8→K10; P2/P3→KHZ; P4/P5/P6→MHZ; P7/P8→GHZ.
- **Displays:** Four common-cathode displays have their two common pins joined, then one 220 Ω resistor per digit return to GND, following the PDF topology and your instruction. Segment nets `a1`–`g4` connect the four 4511 drivers to their matching display segments. Decimal points are intentionally unused.
- **Control and selector nets:** U22 parallel data pins are tied to GND; `a/b/c`, `up`, `down`, and `grid` are labelled. U6 feedback/control labels and the U19/U20 7474 chain are wired as represented in the reference-derived draft. J2 exposes the external logic nets in order: pin 1=`16`, 2=`15`, 3=`14`, 4=`13`, 5=`12`, 6=`uuu`, 7=`grid`, 8=`y`. These external signals must share the board's GND reference.
- **Power:** U28 is an L7805CV in a TO-220-3 footprint. J1 provides the two-pin DC input (`VIN`, GND); C1 is 330 nF and C2 is 100 nF. The regulator output is the shared VCC rail and all placed IC power units are connected to VCC/GND.
- **Indicator LEDs:** D1–D4 each have a 1 kΩ series resistor to GND and are labelled P1/KHZ/MHZ/GHZ.

## Validation and remaining cautions

The final schematic was exported through KiCad CLI to both netlist and PDF, and ERC reports **0 errors and 57 warnings**. All schematic components currently have footprint assignments, and the final netlist confirms the key power, oscillator, display-return, U18/U21/U22, and J2 nets. The 57 warnings are KiCad's 31 embedded-symbol/library mismatch notices and 26 notices for unplaced multi-unit logic sections and their inputs; these are not connectivity errors, but unused physical package sections and their unused inputs should be reviewed before PCB fabrication.

**Do not power or fabricate without electrical and mechanical review.** The 220 Ω resistors are shared common-cathode returns as in the PDF; this is not the usual per-segment current-limiting arrangement, so calculate worst-case display current and verify brightness/driver limits. Confirm the 7805 input voltage, load current, heat dissipation, bypass-capacitor placement, the actual connector types, and each component package. The J2 logic source must be referenced to circuit GND. This is a verified schematic/netlist reconstruction, not a tested physical prototype.
