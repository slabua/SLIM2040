# SLIM2040 (DRAFT)
###### tags: `SLBLabs` `SLB Labs` `SLIM2040` `Raspberry Pi` `RaspberryPi` `Raspberry` `Pi` `Pico` `RaspberryPiPico` `RP2040` `MicroPython` `CircuitPython` `Arduino` `C/C++`

## A RP2040-based dev board with some quirks
SLIM2040 is a custom development board based on the the **RP2040** chip.  
It comes in a slim form factor and some notable additional features.

![SLIM2040-R2.1](https://github.com/user-attachments/assets/b5ca9cd2-89fd-4237-9973-79c1eeddc662)

### Features

- **Power supply in the range 4.5~28V**
  - Convenient and easy integration in industrial environments.
  - Can be powered directly by PLCs and other common industrial devices working in the same DC range, including the regular USB.
- **Reverse polarity protection**
  - A Schottky diode to protect from reverse polarity.
  - Can be bypassed by shorting the appropriate pad on the back of the board if more current is needed.
- **Two user buttons**
  - Convenient and easy operation.
  - Can be used as a controller for sensors or actuators.
- **Power LED, User LED and RGB LED**
  - Convenient and easy way to have a quick glimpse on the status of the system.
- **Qwiic/StemmaQT connector**
  - Convenient and easy way to connect and swap out I2C peripherals such as sensors, etc.
- **Designed to pair with an SSD1306 128 × 32 px OLED Display**
  - Convenient visualisation of data, values or parameters directly on the device.
- **Two dedicated GPIO for high voltage operation**
  - Convenient and easy integration in industrial environments.
  - To send and read digital data from PLCs, etc.

![SLIM2040-R2.1](https://github.com/user-attachments/assets/38ab0961-8758-47c1-b9d5-c666cb544d3d)



[^Top](#Top)


---
## SLIM2040 Rev 2.1 Overview

|Front|Back|
|:-:|:-:|
|![Front](https://github.com/user-attachments/assets/9c3fca01-7641-43c3-bfc6-c7f7fb45bce7)|![Back](https://github.com/user-attachments/assets/6cb30ddc-858a-4dd7-b6d1-69b7b77cc76c)|


### Specifications
| Component | Description |
| -------- | -------- |
| Board form factor: | 48 × 16 mm |
| Power, data transfer: | Micro USB Type-B interface |
| Power Supply: | 4.5~28V via the USB connector or the provided solder pads |
| Polarity protection: | 40V/1A Schottky diode, shortable via solder pad |
| Storage: | 2MB QSPI flash |
| Interfacing: | 16 × Total GPIO available via solder pads |
|          | 2 × high-voltage GPIO for industrial integration |
|          | 14 × supporting PWM |
|          | 1 × 12-bit ADC channels |
| Peripherals: | I2C0 via JST-SH/Qwiic/StemmaQT connector |
|          | I2C0 via through hole pads for SSD1306 128 × 32 px OLED |
|          | I2C1 via solder pads |
|          | SPI0 via solder pads |
|          | UART0 via solder pads |
|          | UART1 via solder pads |
|          | SWC/SWD solder pads |
| LED:     | 1 × Power LED |
|          | 1 × User LED, PWM controllable |
|          | 1 × User WS2812B Neopixel RGB LED (w/ daisychain pad) |
| Buttons: | 1 × BOOTSEL button - SW1 (doubles up as user input button) |
|          | 1 x User button - SW2 |
|          | 1 × Reset button - SW3 |
| Software compatibility: | Micropython ・ CircuitPython ・ C/C++ ・ Arduino |
| Dimensions: | Approximately 49 × 17 × 6 mm (w/ USB port, buttons) |
|          | Approximately 49 × 17 × 9 mm (w/ USB port, buttons, OLED) |

### GPIO Solder Pads Pinout
| GPIO | PWM | I2C | SPI | UART | HV-GPIO |
| :----: | :---: | :---: | :---: | :----: | :----: |
|   0  | PWM0A | SDA0 |  RX0 |  TX0 | - |
|   1  | PWM0B | SCL0 |  CS0 |  RX0 | - |
|   2  | PWM1A | SDA1 | SCK0 | CTS0 | - |
|   3  | PWM1B | SCL1 |  TX0 | RTS0 | - |
|   4  | PWM2A | SDA0 |  RX0 |  TX1 | - |
|   5  | PWM2B | SCL0 |  CS0 |  RX1 | - |
|  10  | PWM5A | SDA1 | SCK1 | CTS1 | - |
|  11  | PWM5B | SCL1 |  TX1 |  TX1 | - |
|  12  | PWM6A | SDA0 |  RX1 |  TX0 | - |
|  16  | PWM0A | SDA0 |  RX0 |  TX0 | - |
|  17  | PWM0B | SCL0 |  CS0 |  RX0 | - |
|  18  | PWM1A | SDA1 | SCK0 | CTS0 | - |
|  19  | PWM1B | SCL1 |  TX0 | RTS0 | - |
|  23  |  -  |   -  |   -  |   -  | OUT |
|  24  |  -  |   -  |   -  |   -  |  IN |
|  26  | PWM5A | SDA1 | SCK1 | CTS1 | - |

### Additional GPIO Information
- I2C0 connector on GPIO16, GPIO17
- User button on GPIO20
- User WS2812B Neopixel RGB LED on GPIO21
- ADC0 on GPIO26
- `GPIO23 = Pin(23, Pin.OUT, Pin.PULL_DOWN)`
- `GPIO24 = Pin(24, Pin.IN, Pin.PULL_UP)`

※ In order for the BOOTSEL button to be recognised as a User button, use: `rp2.bootsel_button()`.  
※ High-voltage GPIOs make use of N-Channel MOSFETs.  
※ OUT pad can switch a maximum of 30V.  
※ IN pad control signal can be up to 12V.  
※ All the GPIOs except those labeled as high-voltage (HV) operate in the regular 3.3V limit regardless of the input power voltage.

### Resources
Product page: git? slblabs? elecrow?

[^Top](#Top)


---
# Notes on the RP2040 Microcontroller
At the very core of the board there is the RP2040 chip.
![](https://www.raspberrypi.com/documentation/microcontrollers/images/rp2040.jpg)

Here follows a list of its major characteristics:

| Component | Description |
| -------- | -------- |
| CPU:     | Dual ARM Cortex-M0+ @ 133 MHz |
| Memory:  | 264kB on-chip SRAM in six independent banks |
| Storage: | Support for up to 16MB of off-chip Flash memory via QSPI bus |
| Architecture: | DMA controller |
|          | Fully connected AHB crossbar |
|          | Interpolator and integer divider peripherals |
|          | On-chip programmable LDO to generate core voltage |
|          | 2 × on-chip PLLs to generate USB and core clocks |
| Interfacing: | 30 × GPIO pins, 4 of which can be used as analogue inputs |
| Peripherals: | 2 × UARTs |
|          | 2 × SPI controllers |
|          | 2 × I2C controllers |
|          | 16 × PWM channels |
|          | 1 × USB 1.1 controller and PHY, with host and device support |
|          | 8 × PIO state machines |
| Package: | 7 × 7 mm QFN-56 package |

Other properties include:
* Supported input power 1.8–5.5V DC
* Operating temperature -40°C to +85°C
* Drag-and-drop programming using mass storage over USB
* Low-power sleep and dormant modes
* Accurate on-chip clock
* Temperature sensor
* Accelerated integer and floating-point libraries on-chip

### RP2040 Pinout
![](https://i.imgur.com/Y8JRuFW.png)

### Resources
https://www.raspberrypi.com/products/rp2040/specifications/  
https://www.raspberrypi.com/documentation/microcontrollers/rp2040.html  
https://datasheets.raspberrypi.com/rp2040/rp2040-product-brief.pdf  
https://datasheets.raspberrypi.com/rp2040/rp2040-datasheet.pdf  

[^Top](#Top)


---
# Notes

※ 

[^Top](#Top)
