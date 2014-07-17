INTRODUCTION
============

What is arduino?
----------------
Arduino is an open-source electronics prototyping platform. It's intended for
artists, designers, hobbyists and anyone interested in creating interactive
objects or environments but that too expensive ($15) for small projects or
if you are new to electronics.We started exploring Digispark project which
has developed around  9$ ATtiny-85 Arduino compatible board.
We have redesigned the circuit with optimized components and used DIP packages
and single sided PCB to reduce cost to less than 3$.

Anuduino
--------

It is micro-sized, Arduino enabled, usb development board - cheap enough to
jumpstart electronics. It is easy to make Do It Yourself project either using
its kicad files or on breadboard.


Difference between arduino and anuduino
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

ArduinoUNO uses ATmega328 microcontroller with 32Kb of flash memory of which
5Kb is used by the bootloader whereas anuduino has 8Kb of flash memory with
2Kb occupied by bootloader,so you have around **6Kb** of memory left for code.


 +------------------------+------------+----------+
 |       Memory           | Anuduino   |ArduinoUNO|
 |                        |            |          |
 +========================+============+==========+
 |Flash(Total)            | 8k bytes   | 32k bytes|
 +------------------------+------------+----------+
 |Flash(Bootloader)       |  2k bytes  |  5k bytes|
 +------------------------+------------+----------+
 |Static RAM              | 512 byte   |  2k bytes|
 +------------------------+------------+----------+
 |EEPROM                  |  512 byte  |  1k byte |
 +------------------------+------------+----------+

|
|
|

 +------------------------+------------+----------+
 |       PINS             | Anuduino   |ArduinoUNO|
 |                        |            |          |
 +========================+============+==========+
 |Total                   |8           |32        |
 +------------------------+------------+----------+
 |Total I/O               |6           |23        |
 +------------------------+------------+----------+
 |Digital I/O   (PWM)     |6  (3)      |16 (6)    |
 +------------------------+------------+----------+
 |Analog  I/O             |4           |6         |
 +------------------------+------------+----------+

|

.. note :: The above comparison is made with Arduino UNO which is a pretty
		   common.There are other variants of Arduino with more cost, more
   		   memory and features as well.


Anuduino specifications
~~~~~~~~~~~~~~~~~~~~~~~

 + Anuduino is an **ATtiny85** based microcontroller development board with
   USB interface.
 + It uses the familiar Arduino IDE for development.
 + PWM on 3 pins
 + ADC on 4 pins
 + I²C and SPI (vis USI)
 + 6 I/O pins (2 are used for USB only if your program actively communicates
   over USB, otherwise you can use all 6 even if you are programming via USB)
 + 8 KB flash memory (about 6 KB after bootloader)


