# Dactyl Manuform 5x6 - Raspberry Pi Pico Wiring Plan

## Overview
This document provides a comprehensive wiring plan for building a Dactyl Manuform 5x6 keyboard with advanced features using a Raspberry Pi Pico (YD-RP2040) microcontroller.

## Hardware Components
- **Microcontroller**: Raspberry Pi Pico (YD-RP2040)
- **Layout**: 5x6 matrix (30 keys per side)
- **Encoders**: 1x EC11 rotary encoder, 1x mouse scroll wheel encoder
- **Display**: 1x 128x32 OLED (SSD1306)
- **RGB LEDs**: 16x WS2812S LEDs
- **Connectivity**: RJ9 socket for future left side connection
- **Switches**: MX-compatible mechanical switches
- **Diodes**: 1N4148 diodes (one per key)

## Pin Assignment Table

### Raspberry Pi Pico GPIO Assignments

| Function | GPIO Pin | Description |
|----------|----------|-------------|
| **Matrix Rows** |
| Row 0 | GP21 | Top row |
| Row 1 | GP20 | Second row |
| Row 2 | GP19 | Third row |
| Row 3 | GP18 | Fourth row |
| Row 4 | GP17 | Fifth row |
| Row 5 | GP16 | Bottom row (thumb cluster) |
| **Matrix Columns** |
| Col 0 | GP10/GP23 | Leftmost column |
| Col 1 | GP11/GP29 | Second column |
| Col 2 | GP12/GP28 | Third column |
| Col 3 | GP13/GP27 | Fourth column |
| Col 4 | GP14/GP26 | Fifth column |
| Col 5 | GP15/GP22 | Rightmost column |
| **Encoders** |
| Rotary Encoder A | GP4 | EC11 encoder pin A |
| Rotary Encoder B | GP5 | EC11 encoder pin B |
| Rotary Encoder SW | GP6 | EC11 encoder button |
| Scroll Encoder A | GP2 | Mouse scroll encoder pin A |
| Scroll Encoder B | GP3 | Mouse scroll encoder pin B |
| **OLED Display** |
| OLED SDA | GP8 | I2C Data line |
| OLED SCL | GP9 | I2C Clock line |
| **RGB LEDs** |
| WS2812S Data | GP7 | RGB LED data line |
| **Split Communication** |
| Split Serial | GP1 | UART TX for split communication |
| Split Serial RX | GP0 | UART RX for split communication |
| **Power & Handedness** |
| Handedness Pin | GP22 | Right/Left detection |
| **Power** |
| VCC | 3V3 | 3.3V power supply |
| GND | GND | Ground |

## Matrix Wiring Diagram

### Right Side (Primary) Matrix Layout
```
    C0    C1    C2    C3    C4    C5
R0  K00   K01   K02   K03   K04   K05
R1  K10   K11   K12   K13   K14   K15
R2  K20   K21   K22   K23   K24   K25
R3  K30   K31   K32   K33   K34   K35
R4  ---   ---   K42   K43   K44   K45  (Thumb cluster)
R5  ---   ---   K52   K53   K54   K55  (Thumb cluster)
```

### Key Switch Wiring
Each key switch requires:
1. **Diode**: Connect cathode (black line) to the row, anode to the switch
2. **Column connection**: Connect switch to column line
3. **Row connection**: Connect through diode to row line

## Component Connections

### 1. OLED Display (128x32 SSD1306)
```
OLED Pin  →  Pi Pico Pin
VCC       →  3V3
GND       →  GND
SDA       →  GP8
SCL       →  GP9
```

### 2. EC11 Rotary Encoder
```
Encoder Pin  →  Pi Pico Pin
A            →  GP4
B            →  GP5
SW (Button) →  GP6
VCC          →  3V3
GND          →  GND
```

### 3. Mouse Scroll Wheel Encoder
```
Encoder Pin  →  Pi Pico Pin
A            →  GP2
B            →  GP3
VCC          →  3V3 (if powered)
GND          →  GND
```

### 4. WS2812S RGB LEDs (16 LEDs)
```
LED Pin  →  Pi Pico Pin
VCC      →  VBUS (5V) or 3V3*
GND      →  GND
DIN      →  GP7
```
*Note: Use 5V for better brightness, but 3.3V works for most WS2812S

**LED Chain Configuration:**
- Connect LEDs in series: DOUT of LED1 → DIN of LED2, etc.
- Total of 16 LEDs for underglow/backlight
- Consider 8 LEDs per side when adding left side

### 5. RJ9 Socket (4P4C) for Split Connection
```
RJ9 Pin  →  Pi Pico Pin  →  Function
1        →  GND          →  Ground
2        →  GP0          →  UART RX
3        →  GP1          →  UART TX  
4        →  VBUS         →  Power (5V)
```

## Power Considerations

### Power Supply Options
1. **USB-C**: Primary power through Pi Pico USB-C port
2. **Battery**: Optional Li-Po battery for wireless operation
3. **Split Power**: Power both sides through RJ9 cable

### Current Requirements
- **Pi Pico**: ~20mA idle, ~40mA active
- **OLED**: ~10-20mA
- **WS2812S LEDs**: ~60mA per LED at full brightness (960mA for 16 LEDs)
- **Total estimated**: ~1.1A at maximum LED brightness

**Recommendation**: Use 5V 2A power supply for full RGB operation.

## Left Side Wiring (Future Expansion)

When adding the left side, use identical wiring but:
1. Mirror the matrix layout
2. Connect via RJ9 cable to right side
3. Use GP22 for handedness detection (tied to GND on left side)

### Left Side Pin Assignments
```
Function         →  GPIO Pin
Matrix Rows      →  GP21-GP16 (same as right)
Matrix Columns   →  GP10-GP15 (same as right)
Split Serial TX  →  GP1
Split Serial RX  →  GP0
Handedness       →  GP22 (tied to GND)
```

## Assembly Steps

### 1. Matrix Assembly
1. Install switches in the 3D printed case
2. Solder diodes to each switch (cathode to row)
3. Wire columns directly to switches
4. Wire rows through diodes
5. Connect matrix to Pi Pico GPIO pins

### 2. Component Installation
1. Mount OLED display and connect I2C lines
2. Install encoders and connect to assigned pins
3. Install WS2812S LED strip and connect data line
4. Install RJ9 socket and wire for split communication

### 3. Testing Procedure
1. Flash test firmware to verify matrix scanning
2. Test OLED display functionality
3. Test encoder rotation and button press
4. Test RGB LED strip
5. Test split communication (when left side is added)

## Troubleshooting

### Common Issues
1. **Matrix not responding**: Check diode orientation and solder joints
2. **OLED blank**: Verify I2C connections and address (0x3C)
3. **RGB LEDs not working**: Check data line connection and power supply
4. **Encoder issues**: Verify pin assignments and debouncing in firmware

### Debug Tools
- Multimeter for continuity testing
- Logic analyzer for I2C/SPI debugging
- QMK console for real-time debugging

## Safety Notes
- Use appropriate flux and ventilation when soldering
- Double-check power connections before first power-on
- Use ESD protection when handling Pi Pico
- Keep current draw within Pi Pico specifications 
