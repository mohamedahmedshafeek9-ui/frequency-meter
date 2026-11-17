# IC Inventory — Clock / Display Controller

Grouped by KiCad library part code; quantities from the validated schematic netlist. Datasheet links added per IC (primary = family named in the schematic value; alt = KiCad library-symbol family / 2nd source).

**Total: 26 ICs across 10 KiCad library part codes** (excludes four KCSC02-105 display modules and oscillator Y1).

## IC Summary

| IC code (library) | Schematic value(s) | Qty | Reference designators | Footprint | Function / verification note | Datasheet (schematic value) | Datasheet (alt) |
|---|---|---|---|---|---|---|---|
| 4511 | 4511 | 4 | U9, U14, U16, U23 | `Package_DIP:DIP-16_W7.62mm` | BCD-to-seven-segment latch/decoder/driver — Schematic value is 4511 without a manufacturer/family suffix; confirm the actual part variant. | [TI CD4511B](https://www.ti.com/lit/ds/symlink/cd4511b.pdf) | — |
| 74260 | 74260 | 1 | U18 | `Package_DIP:DIP-14_W7.62mm` | Custom dual 5-input NOR gate — Custom project symbol. User-specified pinout: Gate 1 pins 1,2,3,12,13→5; Gate 2 pins 4,8,9,10,11→6; GND 7, VCC 14. | [National DM74LS260](https://sm0vpo.com/_pdf/74_TTL/74LS260.pdf) | [onsemi SN74LS260](https://static.datasheets.com/doc/4684613-onsemi-sn74ls260d-ds.pdf) |
| 74HC238 | 74HC238 | 1 | U25 | `Package_DIP:DIP-16_W7.62mm` | 3-to-8 decoder/demultiplexer — Library symbol and schematic value both specify 74HC238. | [TI SN74HC238](https://www.ti.com/lit/ds/symlink/sn74hc238.pdf) | — |
| 74HC74 | 74HC74; 7474 | 3 | U6, U19, U20 | `Package_DIP:DIP-14_W7.62mm` | Dual D-type flip-flop — U6 value is 74HC74, while U19/U20 values are 7474; all use the 74HC74 library symbol. Confirm family consistency. | [TI SN74HC74](https://www.ti.com/lit/ds/symlink/sn74hc74.pdf) | — |
| 74LS04 | NOT | 3 | U15, U26, U27 | `Package_DIP:DIP-14_W7.62mm` | Hex inverter — Library symbol is 74LS04; the schematic value is generic NOT. Confirm the actual device code. | [TI SN74LS04](https://www.ti.com/lit/ds/symlink/sn74ls04.pdf) | — |
| 74LS08 | 7408; AND gate (part family unconfirmed); AND | 4 | U7, U12, U13, U21 | `Package_DIP:DIP-14_W7.62mm` | Quad 2-input AND gate — Library symbol is 74LS08; displayed values include 7408 and generic AND labels. Confirm whether standard 7408, 74LS08, or another family is intended. | [TI SN74LS08](https://www.ti.com/lit/ds/symlink/sn74ls08.pdf) | — |
| 74LS151 | 74HC151 | 1 | U5 | `Package_DIP:DIP-16_W7.62mm` | 8-to-1 multiplexer — KiCad library symbol is 74LS151; displayed schematic value says 74HC151. Confirm intended logic family before procurement. | [TI SN74HC151](https://www.ti.com/lit/ds/symlink/sn74hc151.pdf) | [TI SN74LS151](https://www.ti.com/lit/ds/symlink/sn74ls151.pdf) |
| 74LS193 | 74LS193 | 1 | U22 | `Package_DIP:DIP-16_W7.62mm` | Synchronous 4-bit up/down counter — Library symbol and schematic value both specify 74LS193. | [TI SN74LS193](https://www.ti.com/lit/ds/symlink/sn74ls193.pdf) | — |
| 74LS390 | 74HC390 | 7 | U2, U3, U4, U8, U10, U11, U17 | `Package_DIP:DIP-16_W7.62mm` | Dual decade counter — KiCad library symbol is 74LS390; all seven displayed schematic values say 74HC390. Confirm intended logic family before procurement. | [TI SN74HC390](https://www.ti.com/lit/ds/symlink/sn74hc390.pdf) | [TI SN74LS390](https://www.ti.com/lit/ds/symlink/sn74ls390.pdf) |
| L7805 | L7805CV | 1 | U28 | `Package_TO_SOT_THT:TO-220-3_Vertical` | 5 V linear regulator — Schematic value is L7805CV. Confirm manufacturer suffix, input voltage, load, and thermal requirements. | [ST L78](https://www.st.com/resource/en/datasheet/l78.pdf) | — |
| **TOTAL ICs** | Excludes four KCSC02-105 display modules and oscillator Y1. | **26** |  |  |  |  |  |

### Count scope

26 actual ICs across 10 KiCad library part codes. U24/U29/U30/U31 are display modules, not ICs; Y1 is an active oscillator and is not included.

### Part-code caveat

Some schematic Value fields disagree with the embedded KiCad symbol library part. See the detail sheet; confirm the exact logic family before buying parts or fabricating a PCB.

### Excluded U-designated / non-IC parts

| Part | Qty | References | Footprint | Datasheet |
|---|---|---|---|---|
| KCSC02-105 seven-segment display | 4 | U24, U29, U30, U31 | `Display_7Segment:KCSC02-105` | [Kingbright KCSC02-105](http://www.kingbright.com/attachments/file/psearch/000/00/00/KCSC02-105%28Ver.9A%29.pdf) |
| Y1 active oscillator (not U-designated) | 1 | Y1 | `Oscillator_SMD_Abracon_ASE-4Pin_3.2x2.5mm` | [Abracon ASE](https://abracon.com/Oscillators/ASE.pdf) |

## IC Detail — reference-by-reference

One row per physical IC reference from the KiCad netlist; count is 1 per reference.

| Ref | IC code (library) | Schematic value | Symbol library:part | Footprint | Qty | Verification note | Datasheet (schematic value) | Datasheet (alt) |
|---|---|---|---|---|---|---|---|---|
| **U2** | 74LS390 | 74HC390 | `74xx:74LS390` | `Package_DIP:DIP-16_W7.62mm` | 1 | KiCad library symbol is 74LS390; all seven displayed schematic values say 74HC390. Confirm intended logic family before procurement. Schematic Value currently: 74HC390. | [TI SN74HC390](https://www.ti.com/lit/ds/symlink/sn74hc390.pdf) | [TI SN74LS390](https://www.ti.com/lit/ds/symlink/sn74ls390.pdf) |
| **U3** | 74LS390 | 74HC390 | `74xx:74LS390` | `Package_DIP:DIP-16_W7.62mm` | 1 | KiCad library symbol is 74LS390; all seven displayed schematic values say 74HC390. Confirm intended logic family before procurement. Schematic Value currently: 74HC390. | [TI SN74HC390](https://www.ti.com/lit/ds/symlink/sn74hc390.pdf) | [TI SN74LS390](https://www.ti.com/lit/ds/symlink/sn74ls390.pdf) |
| **U4** | 74LS390 | 74HC390 | `74xx:74LS390` | `Package_DIP:DIP-16_W7.62mm` | 1 | KiCad library symbol is 74LS390; all seven displayed schematic values say 74HC390. Confirm intended logic family before procurement. Schematic Value currently: 74HC390. | [TI SN74HC390](https://www.ti.com/lit/ds/symlink/sn74hc390.pdf) | [TI SN74LS390](https://www.ti.com/lit/ds/symlink/sn74ls390.pdf) |
| **U5** | 74LS151 | 74HC151 | `74xx:74LS151` | `Package_DIP:DIP-16_W7.62mm` | 1 | KiCad library symbol is 74LS151; displayed schematic value says 74HC151. Confirm intended logic family before procurement. Schematic Value currently: 74HC151. | [TI SN74HC151](https://www.ti.com/lit/ds/symlink/sn74hc151.pdf) | [TI SN74LS151](https://www.ti.com/lit/ds/symlink/sn74ls151.pdf) |
| **U6** | 74HC74 | 74HC74 | `74xx:74HC74` | `Package_DIP:DIP-14_W7.62mm` | 1 | U6 value is 74HC74, while U19/U20 values are 7474; all use the 74HC74 library symbol. Confirm family consistency. This reference's Value is: 74HC74. | [TI SN74HC74](https://www.ti.com/lit/ds/symlink/sn74hc74.pdf) | — |
| **U7** | 74LS08 | 7408 | `74xx:74LS08` | `Package_DIP:DIP-14_W7.62mm` | 1 | Library symbol is 74LS08; displayed values include 7408 and generic AND labels. Confirm whether standard 7408, 74LS08, or another family is intended. This reference's Value is: 7408. | [TI SN74LS08](https://www.ti.com/lit/ds/symlink/sn74ls08.pdf) | — |
| **U8** | 74LS390 | 74HC390 | `74xx:74LS390` | `Package_DIP:DIP-16_W7.62mm` | 1 | KiCad library symbol is 74LS390; all seven displayed schematic values say 74HC390. Confirm intended logic family before procurement. Schematic Value currently: 74HC390. | [TI SN74HC390](https://www.ti.com/lit/ds/symlink/sn74hc390.pdf) | [TI SN74LS390](https://www.ti.com/lit/ds/symlink/sn74ls390.pdf) |
| **U9** | 4511 | 4511 | `4xxx_IEEE:4511` | `Package_DIP:DIP-16_W7.62mm` | 1 | Schematic value is 4511 without a manufacturer/family suffix; confirm the actual part variant. | [TI CD4511B](https://www.ti.com/lit/ds/symlink/cd4511b.pdf) | — |
| **U10** | 74LS390 | 74HC390 | `74xx:74LS390` | `Package_DIP:DIP-16_W7.62mm` | 1 | KiCad library symbol is 74LS390; all seven displayed schematic values say 74HC390. Confirm intended logic family before procurement. Schematic Value currently: 74HC390. | [TI SN74HC390](https://www.ti.com/lit/ds/symlink/sn74hc390.pdf) | [TI SN74LS390](https://www.ti.com/lit/ds/symlink/sn74ls390.pdf) |
| **U11** | 74LS390 | 74HC390 | `74xx:74LS390` | `Package_DIP:DIP-16_W7.62mm` | 1 | KiCad library symbol is 74LS390; all seven displayed schematic values say 74HC390. Confirm intended logic family before procurement. Schematic Value currently: 74HC390. | [TI SN74HC390](https://www.ti.com/lit/ds/symlink/sn74hc390.pdf) | [TI SN74LS390](https://www.ti.com/lit/ds/symlink/sn74ls390.pdf) |
| **U12** | 74LS08 | 7408 | `74xx:74LS08` | `Package_DIP:DIP-14_W7.62mm` | 1 | Library symbol is 74LS08; displayed values include 7408 and generic AND labels. Confirm whether standard 7408, 74LS08, or another family is intended. This reference's Value is: 7408. | [TI SN74LS08](https://www.ti.com/lit/ds/symlink/sn74ls08.pdf) | — |
| **U13** | 74LS08 | AND gate (part family unconfirmed) | `74xx:74LS08` | `Package_DIP:DIP-14_W7.62mm` | 1 | Library symbol is 74LS08; displayed values include 7408 and generic AND labels. Confirm whether standard 7408, 74LS08, or another family is intended. This reference's Value is: AND gate (part family unconfirmed). | [TI SN74LS08](https://www.ti.com/lit/ds/symlink/sn74ls08.pdf) | — |
| **U14** | 4511 | 4511 | `4xxx_IEEE:4511` | `Package_DIP:DIP-16_W7.62mm` | 1 | Schematic value is 4511 without a manufacturer/family suffix; confirm the actual part variant. | [TI CD4511B](https://www.ti.com/lit/ds/symlink/cd4511b.pdf) | — |
| **U15** | 74LS04 | NOT | `74xx:74LS04` | `Package_DIP:DIP-14_W7.62mm` | 1 | Library symbol is 74LS04; the schematic value is generic NOT. Confirm the actual device code. This reference's Value is: NOT. | [TI SN74LS04](https://www.ti.com/lit/ds/symlink/sn74ls04.pdf) | — |
| **U16** | 4511 | 4511 | `4xxx_IEEE:4511` | `Package_DIP:DIP-16_W7.62mm` | 1 | Schematic value is 4511 without a manufacturer/family suffix; confirm the actual part variant. | [TI CD4511B](https://www.ti.com/lit/ds/symlink/cd4511b.pdf) | — |
| **U17** | 74LS390 | 74HC390 | `74xx:74LS390` | `Package_DIP:DIP-16_W7.62mm` | 1 | KiCad library symbol is 74LS390; all seven displayed schematic values say 74HC390. Confirm intended logic family before procurement. Schematic Value currently: 74HC390. | [TI SN74HC390](https://www.ti.com/lit/ds/symlink/sn74hc390.pdf) | [TI SN74LS390](https://www.ti.com/lit/ds/symlink/sn74ls390.pdf) |
| **U18** | 74260 | 74260 | `Clock_Reconstruction:74260` | `Package_DIP:DIP-14_W7.62mm` | 1 | Custom project symbol. User-specified pinout: Gate 1 pins 1,2,3,12,13→5; Gate 2 pins 4,8,9,10,11→6; GND 7, VCC 14. | [National DM74LS260](https://sm0vpo.com/_pdf/74_TTL/74LS260.pdf) | [onsemi SN74LS260](https://static.datasheets.com/doc/4684613-onsemi-sn74ls260d-ds.pdf) |
| **U19** | 74HC74 | 7474 | `74xx:74HC74` | `Package_DIP:DIP-14_W7.62mm` | 1 | U6 value is 74HC74, while U19/U20 values are 7474; all use the 74HC74 library symbol. Confirm family consistency. This reference's Value is: 7474. | [TI SN74HC74](https://www.ti.com/lit/ds/symlink/sn74hc74.pdf) | — |
| **U20** | 74HC74 | 7474 | `74xx:74HC74` | `Package_DIP:DIP-14_W7.62mm` | 1 | U6 value is 74HC74, while U19/U20 values are 7474; all use the 74HC74 library symbol. Confirm family consistency. This reference's Value is: 7474. | [TI SN74HC74](https://www.ti.com/lit/ds/symlink/sn74hc74.pdf) | — |
| **U21** | 74LS08 | AND | `74xx:74LS08` | `Package_DIP:DIP-14_W7.62mm` | 1 | Library symbol is 74LS08; displayed values include 7408 and generic AND labels. Confirm whether standard 7408, 74LS08, or another family is intended. This reference's Value is: AND. | [TI SN74LS08](https://www.ti.com/lit/ds/symlink/sn74ls08.pdf) | — |
| **U22** | 74LS193 | 74LS193 | `74xx:74LS193` | `Package_DIP:DIP-16_W7.62mm` | 1 | Library symbol and schematic value both specify 74LS193. | [TI SN74LS193](https://www.ti.com/lit/ds/symlink/sn74ls193.pdf) | — |
| **U23** | 4511 | 4511 | `4xxx_IEEE:4511` | `Package_DIP:DIP-16_W7.62mm` | 1 | Schematic value is 4511 without a manufacturer/family suffix; confirm the actual part variant. | [TI CD4511B](https://www.ti.com/lit/ds/symlink/cd4511b.pdf) | — |
| **U25** | 74HC238 | 74HC238 | `74xx:74HC238` | `Package_DIP:DIP-16_W7.62mm` | 1 | Library symbol and schematic value both specify 74HC238. | [TI SN74HC238](https://www.ti.com/lit/ds/symlink/sn74hc238.pdf) | — |
| **U26** | 74LS04 | NOT | `74xx:74LS04` | `Package_DIP:DIP-14_W7.62mm` | 1 | Library symbol is 74LS04; the schematic value is generic NOT. Confirm the actual device code. This reference's Value is: NOT. | [TI SN74LS04](https://www.ti.com/lit/ds/symlink/sn74ls04.pdf) | — |
| **U27** | 74LS04 | NOT | `74xx:74LS04` | `Package_DIP:DIP-14_W7.62mm` | 1 | Library symbol is 74LS04; the schematic value is generic NOT. Confirm the actual device code. This reference's Value is: NOT. | [TI SN74LS04](https://www.ti.com/lit/ds/symlink/sn74ls04.pdf) | — |
| **U28** | L7805 | L7805CV | `Regulator_Linear:L7805` | `Package_TO_SOT_THT:TO-220-3_Vertical` | 1 | Schematic value is L7805CV. Confirm manufacturer suffix, input voltage, load, and thermal requirements. | [ST L78](https://www.st.com/resource/en/datasheet/l78.pdf) | — |

### Not counted as ICs

| Reference(s) | Device | Qty | Reason | Datasheet |
|---|---|---|---|---|
| U24, U29, U30, U31 | KCSC02-105 display modules | 4 | Seven-segment display components are U-designated, but are not ICs. | [Kingbright KCSC02-105](http://www.kingbright.com/attachments/file/psearch/000/00/00/KCSC02-105%28Ver.9A%29.pdf) |
| Y1 | 10 MHz four-pin active oscillator | 1 | Timebase oscillator; not included in IC count. | [Abracon ASE](https://abracon.com/Oscillators/ASE.pdf) |

## Notes on datasheet links

- Confirmed via search: 74LS260, KCSC02-105, CD4511B, L78.
- Other TI links and the Abracon ASE link use the manufacturers' standard URL pattern and were not individually opened; if one 404s, search the part number on ti.com / abracon.com.
- `74260` maps to the real **74LS260**; its pinout matches the custom symbol (Gate 1 inputs 1,2,3,12,13 → pin 5; Gate 2 inputs 4,8,9,10,11 → pin 6; GND 7, VCC 14).
- `4511` → **CD4511B** (CMOS 4000-series, 3–18 V), not the 74HC4511.
- KCSC02-105: Kingbright lists a newer Ver.12A (2021-03-30); the link is Ver.9A.
- Confirm the exact logic family (HC vs LS) for 151, 390, 74, 08, 04 before procurement.
