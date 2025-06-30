# 3-Mode-LED-Animation-System-Using-74HC595-Shift-Register-and-Button-Control
# Multi-Mode LED Animation with 7-Segment Display and Daisy-Chained Shift Registers

## Overview

This Arduino project showcases a multi-mode LED animation system with a 7-segment display indicating the active mode. It uses **two 74HC595 shift registers daisy-chained together** to control both the LEDs and the 7-segment display using only **three Arduino pins**. A push button allows users to switch between three different LED animation patterns, with the current mode shown on the 7-segment display.

## Features

- Three unique LED animation patterns
- 7-segment display shows the current pattern number (0–2)
- Single push button to cycle between modes
- **Daisy-chained shift registers** reduce pin usage
- Efficient hardware control using `shiftOut()` function

## Components Used

- Arduino UNO (or compatible)
- 2 x 74HC595 shift registers
- 8 x LEDs with 220Ω resistors
- 1 x 7-Segment Common Cathode Display
- 1 x Push Button
- Breadboard and jumper wires

## Circuit Description

### Daisy-Chained Shift Registers

The two 74HC595 shift registers are connected **in series (daisy-chained)**:
- The **first register** (closest to Arduino) controls the **7-segment display**
- The **second register** controls the **8 LEDs**
- Data is shifted through both registers on each update

**Connections:**
| Register | Pin | Arduino | Purpose                         |
|----------|-----|---------|---------------------------------|
| Both     | 12  | 5       | Latch (`LATCH_PIN`)             |
| Both     | 11  | 6       | Clock (`CLOCK_PIN`)             |
| First    | 14  | 4       | Data In (`DATA_PIN`)            |
| First    | 9   | → Second Reg. Pin 14 | Serial Out to Serial In |
| Both     | 13  | GND     | Output Enable (active LOW)      |
| Both     | 10  | 5V      | Master Reset (kept HIGH)        |
| Both     | 16  | 5V      | Power                           |
| Both     | 8   | GND     | Ground                          |

### Button
- Connected between **pin 3** and **GND**
- Uses `digitalRead(PB)` to detect presses

### Outputs

- **Shift Register 1**: Sends data to the **7-segment display**
- **Shift Register 2**: Sends data to the **8 LEDs**

Data is shifted from right to left, so the first byte in `shiftOut()` goes to the **7-segment display**, and the second goes to the **LEDs**.

## Mode Descriptions

- **Mode 0 (State 0):** Alternating between left and right 4-LED blocks
- **Mode 1 (State 1):** Checkerboard-style LED animation
- **Mode 2 (State 2):** Zig-zag vs inverted zig-zag pattern

Each mode is visually represented on the 7-segment display using standard segment encoding.

## Segment Encodings

Examples used in the code:
| Digit | Binary Code  | Segments Lit (A–G) |
|-------|--------------|--------------------|
| 0     | 0b00111111   | A, B, C, D, E, F    |
| 1     | 0b00000110   | B, C                |
| 2     | 0b01011011   | A, B, G, E, D       |

## How to Use

1. Upload the code to your Arduino.
2. Connect the circuit as described above.
3. Power it on. Mode 0 starts by default.
4. Press the button to switch to the next mode.
5. Observe both the LED animation and mode number on the 7-segment display.



Enjoy building and experimenting with shift registers!

## Example

https://github.com/user-attachments/assets/10fecd4a-1ddd-4a3c-84ce-d722f640c232


