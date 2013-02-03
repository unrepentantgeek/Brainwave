Description
===========
Brainwave is a low cost controller for Reprap 3D printers derived from the well known Sanguinololu. The primary design goal was lower cost, achieved by providing only the minimum required components for a single extruder printer.  It can be used to drive a cartesian or delta style printer.

Features:
- Small footprint: only 60mm x 79mm!
- 12V power input
- Micro USB connector
- All connectors at edge of board, vertical or right-angle connectors will fit..
- Atmel AT90USB646 microcontroller w/ USB bootloader
- 1, 2, 16 or 32x microstepping @ up to 800mA
- Dual Z-axis connectors
- Optional per channel current attenuation
- Heated bed support with separate power input (up to 24V @ 15A)
- Integrated heater/thermistor/stepper connector for E channel
- Fan control

Instructions
============
1. Build, buy or borrow a Brainwave
2. Install Arduino 1.0.2
3. install the brainwave arduino hardware bundle from
   [github.com/unrepentantgeek/brainwave-arduino](http://github.com/unrepentantgeek/brainwave-arduino)
   into the Arduino hardware directory.
4. Get Marlin. I am maintaining a branch of Marlin that will compile for
   brainwave at [github.com/unrepentantgeek/Marlin](http://github.com/unrepentantgeek/Marlin/tree/brainwave)
   Marlin HEAD has support, but it doesn't always compile cleanly for this
   board.

Hardware configuration
----------------------
1. Set micro-stepping selector jumpers (D1, D2) per channel.  Short both for 32x
   microstepping.  See table on back of board for other configurations.
   <b>Default: single-step.</b>
2. Set stepper current reference voltages.  I = V / 2.55
   <b>Default: 1V == 400mA.</b>

Software configuration
----------------------

Open Arduino, find the Marlin directory and open Marlin.ino. Select 'Brainwave'
from the Board menu. Find the Configuration.h file and change
DEFAULT_AXIS_STEPS_PER_UNIT to suit your printer (remember, 32x microsteps!)
Power on the Brainwave and connect the USB cable (note: the brainwave will not
power up off USB, you need the 12V supply.) Hold down the PROGRAM button and
press RESET, the STATUS led should pulse. Press the Upload button in Arduino.
After a reset the brainwave will show up as a CDC ACM serial device
(/dev/ttyACM[0..9] on Linux) and be ready to accept commands.

Brandon Bowman wrote up an excellent guide for getting the board working under
Windows and MacOS:
[fabbersuw.blogspot.com/2012/12/if-your-brainwaves-got-no-brains-or.html](http://fabbersuw.blogspot.com/2012/12/if-your-brainwaves-got-no-brains-or.html)

Known issues
------------
- It may take a couple of presses of the RESET button to get the firmware to
  come up after flashing.
- You may need a thermistor or similar 100k resistance present across the bed
  and extruder thermistor inputs. Otherwise Marlin may go into a deathloop and
  you'll never even see a serial device. Even if it doesn't fall on it's face it
  will only sit and complain about too high temp.
- Marlin may lose/gain steps on the X axis.  If so swap X and E to limit the
  impact.  This has not been observed with Sprinter.  The issue is being
  investigated.

Special thanks
--------------
Julie Atwood
Matt Westervelt
Frederik Hubinette
Silas Snider
Johann Rocholl
JP Sugarbroad
Austin Appleby
Richard DeLeon
Plamena Milusheva
Mark Ganter
Brandon Bowman