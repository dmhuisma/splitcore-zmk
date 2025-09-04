# Splitcore Keyboard ZMK Module

WORK IN PROGRESS

This is my ZMK module for the split keyboard I generated with the [Cosmos keyboard generator](https://ryanis.cool/cosmos/). It is the successor to the [Dmhuisma keyboard](https://github.com/dmhuisma/dmhuisma-keyboard-zmk-module), with the main goal of reducing the height for better ergonomics, improving the thumb cluster/dpad, and better pointing capabilities.

The cosmos generator configuration is saved in the URL, here is [my configuration](https://ryanis.cool/cosmos/beta#cm:CugBChwSBRCAbyAnEgIgExICIAASADgeQICmi4AFSLMDCiUSBRCAYyAnEgIgExICIAASAxCwOxIJELBrIChIgowEOApAgMhdCiMSBRCAVyAnEgIgExICIAASAxCwLxIFELBfICg4CUCAkIfYAgoTEgUQgEsgJxICIBMSAiAAEgA4HQoTEgUQgD8gJxICIBMSAiAAEgA4MQofEgIgJxICIBMSBhCggAogABICEDA4MkCApouABUizAwoiEgQQECATEgoIGyAAQIKShsgDMB04RUCjkvABSPKJrKyBDBgAQOiFoK7wVUjc8KKgAQpwChASBhBAIA5AARIEIAVAATgTCiESEQiBMBDAgAJAAUiAgIz9A1ByEgoIgCAQQEABUIUBOAAKHBIPCIAwEEBAAUiAgIz9A1BaEgcIgCAgD0ABOBQYAiIKCMgBEMgBGAAgAEDXicymkDZIqY2AtvGXHAq8AQocEgUQgAMgJxICIBMSAiAAEgA4HUCApouABUizAwoeEgUQgA8gJxICIBMSAiAAEgASBRCwayAoOAlAgMhdCiASBRCAGyAnEgIgExICIAASABIFELBfICg4CkCAkIfYAgoVEgUQgCcgJxICIBMSAiAAEgA4HkAAChMSBRCAMyAnEgIgExICIAASADgyCh8SAiAnEgIgExIGEKCACiAAEgIQMDgxQICmi4AFSLMDGAFA54WgrvBVSNzuopgBEAMYhiAiBgjNARDDATgDggEDgwEAWEhgA2gAcgYoMjgKQBR4gomklLE3). It also provides the BOM for this keyboard.

## Features
- Ergonomic
    - Split
    - Concave key well
    - Thumb clusters
    - Staggered to accommodate my hand/finger sizes
- Wireless
- Mouse control (exact method TBD, perhaps trackpoint or joystick).
- Display
- Hotswappable keys
- Potentiometer (one with directional clicking) for media controls.
- Dpad for cursor navigation or gaming, custom design.

## Building

The firmware is built by Github actions on every commit. It can also be built with a local install of ZMK with the following commands.

> west build -p auto -d build/left -b nice_nano_v2 -- -DZMK_EXTRA_MODULES="[path to module]/splitcore-zmk;" -DSHIELD="splitcore_left"

> west build -p auto -d build/right -b nice_nano_v2 -- -DZMK_EXTRA_MODULES="[path to module]/splitcore-zmk;" -DSHIELD="splitcore_right nice_view"

## Keyscan Matrix

TODO

## Pinout

This keyboard uses the [nice!nano V2](https://nicekeyboards.com/nice-nano/) on each side. However, there is not enough GPIO pins for this keyboard, so it also uses shift registers (74HC595) for the output pins.

### Left Keyboard

#### Nice!Nano V2 Left Side GPIO
|                       |                                               |
|-----------------------|-----------------------------------------------|
|Battery-               ||
|**[D1]** P0.06         ||
|**[D0]** P0.08         ||
|GND                    ||
|GND                    |DPAD GND|
|**[D2]** P0.17         ||
|**[D3]** P0.20         ||
|**[D4]** P0.22         ||
|**[D5]** P0.24         ||
|**[D6]** P1.00         |DPAD Up|
|**[D7]** P0.11         |DPAD Down|
|**[D8]** P1.04         |DPAD Left|
|**[D9]** P1.06         |DPAD Right|

#### Nice!Nano V2 Right Side GPIO
|                       |                                               |
|-----------------------|-----------------------------------------------|
|Battery+               ||
|Battery+               ||
|GND                    |74HC595 GND, 74HC595 OE|
|Reset                  ||
|3.3V Vcc               |74HC595 Vcc|
|**[D21]** P0.31 (ADC)  |Row 1|
|**[D20]** P0.29 (ADC)  |Row 2|
|**[D19]** P0.02 (ADC)  |Row 3|
|**[D18]** P1.15        |Row 4|
|**[D15]** P1.13        |74HC595 SCK|
|**[D14]** P1.11        ||
|**[D16]** P0.10        |74HC595 MOSI|
|**[D10]** P0.09        |74HC595 CS/RCLK|

#### Nice!Nano V2 Back GPIO
|                       |                                               |
|-----------------------|-----------------------------------------------|
|P1.01                  ||
|P1.02                  ||
|P1.07                  ||

#### Shift Register (74HC595) GPIO
|                       |                                               |
|-----------------------|-----------------------------------------------|
|QA                     |Column 1|
|QB                     |Column 2|
|QC                     |Column 3|
|QD                     |Column 4|
|QE                     |Column 5|
|QF                     |Column 6|
|QG                     |Column 7|
|QH                     |Column 8|
|QH`                    ||

### Right Keyboard

#### Nice!Nano V2 Left Side GPIO
|                       |                                               |
|-----------------------|-----------------------------------------------|
|Battery+               ||
|**[D1]** P0.06         |RKJXT1F42001 Encoder A|
|**[D0]** P0.08         |RKJXT1F42001 Encoder B|
|GND                    |NiceView GND|
|GND                    |RKJXT1F42001 GND|
|**[D2]** P0.17         ||
|**[D3]** P0.20         ||
|**[D4]** P0.22         |NiceView CS|
|**[D5]** P0.24         |RKJXT1F42001 up|
|**[D6]** P1.00         |RKJXT1F42001 down|
|**[D7]** P0.11         |RKJXT1F42001 left|
|**[D8]** P1.04         |RKJXT1F42001 right|
|**[D9]** P1.06         |RKJXT1F42001 center|

#### Nice!Nano V2 Right Side GPIO
|                       |                                               |
|-----------------------|-----------------------------------------------|
|Battery+               ||
|Battery+               ||
|GND                    |74HC595 GND, 74HC595 OE|
|Reset                  ||
|3.3V Vcc               |NiceView Vcc, 74HC595 Vcc|
|**[D21]** P0.31 (ADC)  |Row 1|
|**[D20]** P0.29 (ADC)  |Row 2|
|**[D19]** P0.02 (ADC)  |Row 3|
|**[D18]** P1.15        |Row 4|
|**[D15]** P1.13        |74HC595 SCK, NiceView SCK|
|**[D14]** P1.11        ||
|**[D16]** P0.10        |74HC595 MOSI, NiceView MOSI|
|**[D10]** P0.09        |74HC595 CS/RCLK|

#### Nice!Nano V2 Back GPIO
|                       |                                               |
|-----------------------|-----------------------------------------------|
|P1.01                  ||
|P1.02                  ||
|P1.07                  ||

#### Shift Register (74HC595) GPIO
|                       |                                               |
|-----------------------|-----------------------------------------------|
|QA                     |Column 1|
|QB                     |Column 2|
|QC                     |Column 3|
|QD                     |Column 4|
|QE                     |Column 5|
|QF                     |Column 6|
|QG                     |Column 7|
|QH                     |Column 8|
|QH`                    ||

### Nice!Nano V2 pinout for reference

![Nice!Nano V2 Pinout](https://nicekeyboards.com/static/1788ac663060fd510f4894b286cd97b1/a6d36/pinout-v2.png)
