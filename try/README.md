# KiCad clock/display schematic reconstruction (draft)

## Files

- `clock_display_visual_draft.kicad_sch` — a KiCad-native, editable schematic sheet with the components arranged in approximate groups based on the supplied screenshot.

## Important: this is not a functioning circuit

This is a **visual component-layout reconstruction only**. The source was a raster screenshot, and the image does not reliably reveal all pin numbers, wire crossings, or net junctions. To avoid inventing connectivity, **no electrical wires or nets have been added**. The sheet itself carries warnings to that effect. Do not fabricate or power a circuit from this draft.

Before using it as a design, a KiCad user must reconstruct and verify every connection, power rail, reset/clock path, display polarity, and resistor value, then run ERC and inspect the generated netlist.

## Approximation notes

- The screenshot labels several counters and logic parts `74HC390`/`74HC151`; this sheet uses the bundled KiCad `74LS390`/`74LS151` symbol shapes as cached visual stand-ins and changes the visible value text to match the screenshot. Confirm the actual part variants and pinouts.
- The screenshot identifies `U18` as a `74LS260`, but the bundled symbol library used to generate this draft did not contain that symbol. `U18` is therefore a visibly labelled **74LS02 placeholder**. Replace it with the correct 74LS260 symbol and verify its pins before wiring.
- `MAN72A` is used for each of the four display digits as a convenient single-digit symbol. The actual display part and common-anode/common-cathode polarity are unknown.
- The four `R_Network08` symbols are visual stand-ins. Values and network topology are unknown.
- The AND/NOT gates and other part-family details are inferred from the labels/shapes and should be checked against the source design.
- No ERC was run: this sandbox has the KiCad symbol libraries but not the KiCad desktop/CLI application. The supplied Windows path was not accessible from this sandbox.

## Opening

Open `clock_display_visual_draft.kicad_sch` directly in KiCad. The sheet embeds the symbol definitions it uses, so the matching global symbol libraries are not required merely to display the cached symbols. The file uses a KiCad 9+ schematic format.
