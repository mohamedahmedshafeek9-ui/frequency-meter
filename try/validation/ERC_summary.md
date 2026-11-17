# Final ERC summary — validation run 07

Validated with KiCad CLI 10.0.3 against `validation_run_07/clock_display_visual_draft.kicad_sch` after netlist export.

- **Errors:** 0
- **Warnings:** 57
  - 31 `lib_symbol_mismatch` notices: cached project symbol definitions differ from the current KiCad system library definitions. These are legacy/customized symbol copies, not net connectivity errors.
  - 13 `missing_unit` notices: unused multi-unit gates/counter/flip-flop sections are not drawn on the sheet.
  - 13 `missing_input_pin` notices: the unplaced units above contain input pins that ERC cannot inspect in the schematic.
- **Footprint links:** 0 missing-library or missing-footprint warnings after adding the KiCad 10 aliases and assigning footprints.
- **Blank component footprints in netlist:** none.
- **Netlist export:** successful.

The exported netlist confirms:

- Y1 pin 3 drives `CLK_10M`; pins 1 and 4 are VCC and pin 2 is GND.
- U28 (L7805CV) pin 1 is on `VIN`, pin 2 on GND, and pin 3 on VCC.
- Four display common-cathode pin pairs join through separate 220 Ω return resistors R1/R2/R3/R5 to GND.
- U18 pin 5 drives U21; U21 and U26 route to U22 DOWN.
- U22 data pins are grounded; `a/b/c`, `up`, `down`, and `grid` are net-labelled.
- J2 pins 1–8 map to `16`, `15`, `14`, `13`, `12`, `uuu`, `grid`, and `y`.
- Fourteen 1N4007 diodes implement the PDF matrix groups: K1, K100, K10, KHZ, MHZ, and GHZ.

**Scope:** zero ERC errors verifies the exported schematic connectivity, not physical behavior. Before PCB fabrication, review all 13 unplaced multi-unit sections and ensure any unused physical inputs are safely tied off. Verify the shared 220 Ω display-return current/brightness, the 7805 input voltage and thermal load, and final mechanical packages/connectors.
