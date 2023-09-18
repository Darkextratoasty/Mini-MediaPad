# Mini-MediaPad
A small macropad featuring three keys and a rotary encoder for simple media control. 

## BOM
- [CJMCU Beetle ATmega32U4](https://www.amazon.com/Keyboard-ATMEGA32U4-Development-Arduino-Leonardo/dp/B092D15447) \(probably want to find a different board, this one is pretty obsolete\)
- [Adafruit USB-C Breakout Board](https://www.adafruit.com/product/4090)
- [12mm Square Tact Button](https://www.adafruit.com/product/1010)
- [Rotary Encoder](https://www.adafruit.com/product/377) \(I think this is the right one, I just used one I had laying around\)
- 2x [M2.5x4.5x4.5mm heat-set threaded inserts](https://www.amazon.com/gp/product/B07HKT5W7S/ref=ppx_yo_dt_b_search_asin_title?ie=UTF8&th=1)
- 2x [M2.5x5mm machine screws](https://www.amazon.com/HanTof-Raspberry-Standoffs-Standoff-Cylinder/dp/B07KM27KC6/)
- 8mm Round rubber feet
- 3x Cherry MX style keyswitches
- 4x some kind of diodes \(ex. 1n4007\)
- Either 3x Cherry MX compatible keycaps or print 3x of the Loweredkeycap.stl model
Optional:
- Up to 16 M5x6x7mm heat-set threaded inserts for knob weight
- Up to 16 M5x4mm to M5x10mm machine screws for knob weight
- A 34x60x5mm bar of copper for pad weight \(probably could just glue some nuts or washers in instead\)

## Assembly
### Printed Parts
Print the MediaPad-Top, MediaPad-Bottom, Knob, and 3x Loweredkeycap \(if using printed keycaps\) files. Note that these files are not tolerances at all, so you will need to either adjust your slicer \(horizontal expansion in Cura\) or edit the CAD files and give the models some tolerance. Also, the keycaps are a nightmare to print, require support material, and have a rather unpleasant surface finish, I'd honestly suggest just buying keycaps. If you get everything really tuned in, the components just press fit into the case, requiring no glue, tape, or screws \(except the USB-C breakout, that requires 2x M2.5 threaded inserts and screws\).
### Wiring
The 12mm tact button acts as a reset switch for easily flashing the board. It should be connected to the GND and RES \(reset\) pins. 

The rotary encoder's encoder pins should be connected to MI \(B3\) and MO \(B2\), with the middle pin going to GND. The encoder's button pins act like a fourth keyswitch. You may have to swap the A and B pins in the QMK firmware if the knob seems to go in the wrong direction.

The keys are wired in a ROW2COL, 4x1 matrix, meaning each key's wiring goes from the common row pin, to the keyswitch, to the diode anode, to the key's column pin. The common row pin is A2 \(F5\) and the column pins, going from left to right top view, are key1-A0 \(F7\), key2-D9 \(B5\), key2-D10 \(B6\), and encoder button-D11 \(B7\).

The USB-C breakout is wired to the ATmega32U4 board's USB pins. 

## Flashing the Firmware
Since this is a custom board that isn't supported natively by QMK, you have to either compile the firmware yourself or use the precompiled .hex file in the QMK_Firmware folder. To compile the firmware, you can copy the mini-mediapad folder into your qmk_firmware/keyboards/ directory and run "qmk compile -kb mini_mediapad -km default". I don't plan to submit this to QMK for native support. To flash, press the 12mm tact button under the knob, then use QMK Toolbox or the command line to flash the .hex file to the board.

## Results
Once everything is built and flashed, the keys should do, left to right top view, previous track, play/pause, next track, encoder turn for volume up/down, and encoder press for mute.
