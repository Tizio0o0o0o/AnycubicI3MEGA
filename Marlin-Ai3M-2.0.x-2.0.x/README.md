This is my current firmware, As you can see this is not edited by me, thanks to davidramiro for doing it and introducing me to this firmware editing world.

# Anycubic i3 Mega / Mega-S Marlin 2.0.x by davidramiro

[![Open Issues](https://img.shields.io/github/issues-raw/davidramiro/Marlin-Ai3M-2.0.x.svg?style=flat)](https://github.com/davidramiro/Marlin-Ai3M-2.0.x/issues?q=is%3Aopen+is%3Aissue) [![Closed Issues](https://img.shields.io/github/issues-closed-raw/davidramiro/Marlin-Ai3M-2.0.x.svg?style=flat)](https://github.com/davidramiro/Marlin-Ai3M-2.0.x/issues?q=is%3Aissue+is%3Aclosed) [![Travis CI](https://api.travis-ci.org/davidramiro/Marlin-Ai3M-2.0.x.svg?branch=bugfix-2.0.x)](https://travis-ci.org/davidramiro/Marlin-Ai3M-2.0.x) [![License](https://img.shields.io/github/license/davidramiro/Marlin-Ai3M-2.0.x.svg?style=flat)](https://github.com/davidramiro/Marlin-Ai3M-2.0.x/blob/master/LICENSE)

## Beta build - use with caution!

## Why use this?

While the i3 Mega is a great printer for its price and produces fantastic results in stock, there are some improvements and additional features that this firmware provides:

- Many people have issues getting the Ultrabase leveled perfectly, using Manual Mesh Bed Leveling the printer generates a mesh of the flatness of the bed and compensates for it on the Z-axis for perfect prints without having to level with the screws.
- Much more efficient bed heating by using PID control. This uses less power and holds the temperature at a steady level. Highly recommended for printing ABS.
- Fairly loud fans, while almost every one of them is easily replaced, the stock FW only gives out 9V instead of 12V on the parts cooling fan so some fans like Noctua don't run like they should. This is fixed in this firmware.
- Even better print quality by adding Linear Advance, S-Curve Acceleration and some tweaks on jerk and acceleration.
- Thermal runaway protection: Reducing fire risk by detecting a faulty or misaligned thermistor.
- Very loud stock stepper motor drivers, easily replaced by Watterott or FYSETC TMC2208. To do that, you'd usually have to flip the connectors on the board, this is not necessary using this firmware.
- No need to slice and upload custom bed leveling tests, test it with a single GCode command
- Easily start an auto PID tune or mesh bed leveling via the special menu (insert SD card, select special menu and press the round arrow)
- Filament change feature enabled: Switch colors/material mid print (instructions below) and control it via display.
- The filament runout, pause and stop functionality have been overhauled and improved: The hotend now parks and retracts (on pause or stop) and purges automatically (on resume).
- Added `M888` cooldown routine for the Anycubic Ultrabase (EXPERIMENTAL): This is meant to be placed at the end Gcode of your slicer. It hovers over the print bed and does circular movements while running the fan. Works best with custom fan ducts.
  - Optional parameters:
  - `T<temperature>`: Target bed temperature (min 15°C), 30°C if not specified (do not set this under room temperature)
  - `S<fan speed>`: Fan speed between 0 and 255, full speed if not specified
  - e.g. `M888 S191 T25`: run the fan at 75% until the bed has cooled down to 25°C

## Known issues:

- Power outage support is not included
- Estimated print times from your slicer might be slightly off.
- Special characters on any file or folders name on the SD card will cause the file menu to freeze. Simply replace or remove every special character (Chinese, Arabic, Russian, accents, German & Scandinavian umlauts, ...) from the name. Symbols like dashes or underscores are no problem.
  **Important note: On the SD card that comes with the printer there is a folder with Chinese characters in it by default. Please rename or remove it.**

## Marlin 2.0

Marlin 2.0 takes this popular RepRap firmware to the next level by adding support for much faster 32-bit and ARM-based boards while improving support for 8-bit AVR boards. Read about Marlin's decision to use a "Hardware Abstraction Layer" below.

Download earlier versions of Marlin on the [Releases page](https://github.com/MarlinFirmware/Marlin/releases).

## Building Marlin 2.0

To build Marlin 2.0 you'll need [Arduino IDE 1.8.8 or newer](https://www.arduino.cc/en/main/software) or [PlatformIO](http://docs.platformio.org/en/latest/ide.html#platformio-ide). Detailed build and install instructions are posted at:

- [Installing Marlin (Arduino)](http://marlinfw.org/docs/basics/install_arduino.html)
- [Installing Marlin (VSCode)](http://marlinfw.org/docs/basics/install_platformio_vscode.html).

### Supported Platforms

| Platform                                                                                                                                                                                                  | MCU            | Example Boards                                  |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------- | ----------------------------------------------- |
| [Arduino AVR](https://www.arduino.cc/)                                                                                                                                                                    | ATmega         | RAMPS, Melzi, RAMBo                             |
| [Teensy++ 2.0](http://www.microchip.com/wwwproducts/en/AT90USB1286)                                                                                                                                       | AT90USB1286    | Printrboard                                     |
| [Arduino Due](https://www.arduino.cc/en/Guide/ArduinoDue)                                                                                                                                                 | SAM3X8E        | RAMPS-FD, RADDS, RAMPS4DUE                      |
| [LPC1768](http://www.nxp.com/products/microcontrollers-and-processors/arm-based-processors-and-mcus/lpc-cortex-m-mcus/lpc1700-cortex-m3/512kb-flash-64kb-sram-ethernet-usb-lqfp100-package:LPC1768FBD100) | ARM® Cortex-M3 | MKS SBASE, Re-ARM, Selena Compact               |
| [LPC1769](https://www.nxp.com/products/processors-and-microcontrollers/arm-microcontrollers/general-purpose-mcus/lpc1700-cortex-m3/512kb-flash-64kb-sram-ethernet-usb-lqfp100-package:LPC1769FBD100)      | ARM® Cortex-M3 | Smoothieboard, Azteeg X5 mini, TH3D EZBoard     |
| [STM32F103](https://www.st.com/en/microcontrollers-microprocessors/stm32f103.html)                                                                                                                        | ARM® Cortex-M3 | Malyan M200, GTM32 Pro, MKS Robin, BTT SKR Mini |
| [STM32F401](https://www.st.com/en/microcontrollers-microprocessors/stm32f401.html)                                                                                                                        | ARM® Cortex-M4 | ARMED, Rumba32, SKR Pro, Lerdge, FYSETC S6      |
| [STM32F7x6](https://www.st.com/en/microcontrollers-microprocessors/stm32f7x6.html)                                                                                                                        | ARM® Cortex-M7 | The Borg, RemRam V1                             |
| [SAMD51P20A](https://www.adafruit.com/product/4064)                                                                                                                                                       | ARM® Cortex-M4 | Adafruit Grand Central M4                       |
| [Teensy 3.5](https://www.pjrc.com/store/teensy35.html)                                                                                                                                                    | ARM® Cortex-M4 |
| [Teensy 3.6](https://www.pjrc.com/store/teensy36.html)                                                                                                                                                    | ARM® Cortex-M4 |

## Submitting Changes

- Submit **Bug Fixes** as Pull Requests to the ([bugfix-2.0.x](https://github.com/MarlinFirmware/Marlin/tree/bugfix-2.0.x)) branch.
- Follow the [Coding Standards](http://marlinfw.org/docs/development/coding_standards.html) to gain points with the maintainers.
- Please submit your questions and concerns to the [Issue Queue](https://github.com/MarlinFirmware/Marlin/issues).

## Marlin Support

For best results getting help with configuration and troubleshooting, please use the following resources:

- [Marlin Documentation](http://marlinfw.org) - Official Marlin documentation
- [Marlin Discord](https://discord.gg/n5NJ59y) - Discuss issues with Marlin users and developers
- Facebook Group ["Marlin Firmware"](https://www.facebook.com/groups/1049718498464482/)
- RepRap.org [Marlin Forum](http://forums.reprap.org/list.php?415)
- [Tom's 3D Forums](https://discuss.toms3d.org/)
- Facebook Group ["Marlin Firmware for 3D Printers"](https://www.facebook.com/groups/3Dtechtalk/)
- [Marlin Configuration](https://www.youtube.com/results?search_query=marlin+configuration) on YouTube

## Credits

The current Marlin dev team consists of:

- Scott Lahteine [[@thinkyhead](https://github.com/thinkyhead)] - USA &nbsp; [Donate](http://www.thinkyhead.com/donate-to-marlin) / Flattr: [![Flattr Scott](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=thinkyhead&url=https://github.com/MarlinFirmware/Marlin&title=Marlin&language=&tags=github&category=software)
- Roxanne Neufeld [[@Roxy-3D](https://github.com/Roxy-3D)] - USA
- Chris Pepper [[@p3p](https://github.com/p3p)] - UK
- Bob Kuhn [[@Bob-the-Kuhn](https://github.com/Bob-the-Kuhn)] - USA
- João Brazio [[@jbrazio](https://github.com/jbrazio)] - Portugal
- Erik van der Zalm [[@ErikZalm](https://github.com/ErikZalm)] - Netherlands &nbsp; [![Flattr Erik](http://api.flattr.com/button/flattr-badge-large.png)](https://flattr.com/submit/auto?user_id=ErikZalm&url=https://github.com/MarlinFirmware/Marlin&title=Marlin&language=&tags=github&category=software)

## License

Marlin is published under the [GPL license](/LICENSE) because we believe in open development. The GPL comes with both rights and obligations. Whether you use Marlin firmware as the driver for your open or closed-source product, you must keep Marlin open, and you must provide your compatible Marlin source code to end users upon request. The most straightforward way to comply with the Marlin license is to make a fork of Marlin on Github, perform your modifications, and direct users to your modified fork.

While we can't prevent the use of this code in products (3D printers, CNC, etc.) that are closed source or crippled by a patent, we would prefer that you choose another firmware or, better yet, make your own.
