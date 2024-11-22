# SLIM2040
###### tags: `SLBLabs` `SLB Labs` `SLIM2040` `Raspberry Pi` `RaspberryPi` `Raspberry` `Pi` `Pico` `RaspberryPiPico` `RP2040` `MicroPython` `CircuitPython` `Arduino` `C/C++`

## A RP2040-based dev board with some quirks
SLIM2040 is a custom development board based on the the **RP2040** chip.  
It comes in a slim form factor and some notable additional features.

### Test Firmware installation

The procedure should work on any OS platform and does not require any particular tool.

1. Connect SLIM2040 to the PC via its USB port.
    - The power led D2 should light up.
    - A removable drive labeled RPI-RP2 should become available.
2. Download and copy the [firmware-test.uf2](./firmware-test.uf2) file into the RPI-RP2 drive.
    - SLIM2040 should reboot.
    - The user led D3 should light up blue.
    - The rgb led D4 should light up red.
3. Hold down the Bootsel/User button SW1.
    - the user led D3 should blink periodically.
4. Hold down the User button SW2.
    - the rgb led D4 should cycle through red, green and blue.
5. Press the reset button SW3.
    - SLIM2040 should return to the initial state described in point 2.
6. Hold down the reset button SW3 while momentarily pressing the bootsel button SW1.
7. Release the reset button SW3.
    - SLIM2040 should return to the state described in point 1.
8. Disconnect SLIM2040.
9. Test completed successfully.
