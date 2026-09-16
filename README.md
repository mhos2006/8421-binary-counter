# 4-Bit BCD Decade Counter

## Overview
This circuit bridges the gap between analog timing and digital sequential logic. It utilizes an NE555 timer configured in astable mode to generate a slow, adjustable ~1 Hz clock pulse. This "heartbeat" drives a 74LS90 decade counter, translating the analog pulses into a physical Binary Coded Decimal (BCD) output displayed across an LED array. 

Due to component availability, a 74LS90 BCD counter was implemented instead of a standard 4-bit binary counter, resulting in a system that counts from 0 to 9 (`0000` to `1001`) before mathematically resetting.

## Hardware Specifications
- **ICs:** 1x NE555 (Astable Clock), 1x 74LS90 (BCD Decade Counter)
- **Controls:** 1x 10kΩ Potentiometer (Clock speed/frequency sweep)
- **Passive Components:** 100µF electrolytic capacitor (timing), 0.1µF ceramic capacitor (comparator stability), assorted 1kΩ resistors.
- **Output:** 5x LEDs (1x Clock Monitor, 4x Binary Output Array)
- **Power:** Strictly 5V DC (LS-Series logic requirement).

## Prerequisites
Because the 74LS90 is an LS-series (Low-power Schottky) logic chip, it is strictly intolerant of voltage fluctuations and cannot be driven directly from raw battery packs. I used a custom multi-cell battery pack regulated to output a stable 5V logic line. 
[5V Linear Breadboard Power Supply](https://github.com/mhos2006/starter-dc-makeshift-power-supply)

## Schematics
<img width="1125" height="202" alt="image" src="[INSERT_KICAD_SCHEMATIC_LINK_HERE]" />

## Testing

- The Red LED is for 1
- The Yellow LED is for 2
- The Green LED is for 4
- The Blue LED is for 8

https://github.com/user-attachments/assets/b8dcc610-90b7-4d0b-bdf6-9d9a19adadde



## Construction Notes & Hardware Quirks
- **The BCD Loop:** To configure the 74LS90 to count properly, its internal bi-quinary flip-flops must be cascaded. This requires a hardwired jumper from Pin 12 (Q0) directly to Pin 1 (CP1). 
- **Floating Reset Traps:** The 74LS90 features four separate master reset pins (Pins 2, 3, 6, and 7). If left floating, ambient electromagnetic noise will randomly freeze the counter. All four must be firmly tied to Ground.
- **Diagnostic Monitor:** A dedicated LED is tapped into the NE555 Pin 3 output before the signal reaches the counter IC. This provides a visual confirmation of the clock speed and isolates debugging if the sequential logic fails.

## Schematic and PCB Documentation
The schematic was drafted using KiCad to document the logic routing. Since the core functionality is contained entirely within the IC architecture, a full technical report was omitted in favor of direct datasheet implementation.
