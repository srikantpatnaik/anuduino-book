Frequently Asked Questions
==========================

What is hex file ?
------------------

A hex file is a way to store data, in this case compiled code for an avr
microcontroller. It is a common file format and something being a hex file
does not mean it can be uploaded on the chip. When you use the Arduino IDE
to upload a file to the board your code is compiled into a hex file and then
uploaded using the command line tool which is built into Arduino.

How micronucleus bootloader works ?
-----------------------------------

Micronucleus is a bootloader designed for AVR tiny 85 chips with a minimal
usb interface.Micronucelus is the code that is installed on the device using
an avr programmer. This  code allows the anuduino to act like a USB device,
receives code, and when it receives code erase the code previously loaded.
It also runs the code loaded onto it after a 5 second  delay (if bootloader
uploaded is normal version , more about this later) if it does not receive a
request to upload new code within that 5 seconds.

It is a small V-USB program, similar to the DigiUSB, DigiKeyboard, and other
usb related libraries. Normally programs exist at the very beginning of  the
flash memory in the attiny85 chip, but micronucleus has been modified so the
start of the program is about 6kb of 0xFF bytes (In other words all the bits
in 6Kb are high). After that, micronucleus begins and uses up the final 2kb.
This leaves room at the start of the chip for your own programs, but micronucleus
always stays installed at the end. 0xFF  bytes are interpreted as NOP (no operation)
instructions by the AVR chip, so the first time you run it, or if you run it after
an erase but no write (sometimes this happens if there  is an error during the
erase part of an upload attempt), next time the chip turns on it will execute
all those NOPs and slam in to the bootloader code.

When you use micronucleus to upload a program, there's a trick to it - USB
requires the device always respond to requests, but the tiny85 chip can't do
that - whenever it's erasing  or writing part of it's own program memory it
has to go to sleep for about 4.5 milliseconds. Some of the more expensive
chips like the mega328 have special bootloader support which lets them keep
running in the background while an erase or write happens in another section
of memory. `Embedded Creations <http://embedded-creations.com/projects/attiny85-usb-bootloader-overview/>`_
discovered however that if you craft your computer  program to just not send
any requests during that frozen time, the computer never notices the device
has frozen up and doesn't crash the USB connection. This is pretty fragile,
which is why the USB connection to the bootloader can sometimes crash if you
run other intense usb software in the background, like an instance of digiterm
polling for a device to appear.

So when the micronucleus command line tool first finds anuduino, it asks it
"How much memory do you have, and how long should I wait after each type of
request?" - when you see that assertion fail on ubuntu, it's talking about
that request - the program tried to ask that question and had an error response
due to linux permissions issues. Next,it asks the device to erase it's memory
and waits the right amount of time for it to do so - about 50 milliseconds to
do all 6kb of flash pages. Once that's done, it starts uploading 64 byte chunks
of your new program. Micronucleus writes in these bytes at the starting 6kb of
flash memory, but with one special exception:

In the first page there's an interrupt vector table. The bootloader (on the
device) replaces the reset vector and the pinchange vector with jump instructions
pointing to it's own interrupt vector table 6kb later. Other than that, the program
is left alone. When the computer is finished uploading, the bootloader finally writes
down what the original values of the user's reset vector and pinchange vector were in
the very last four bytes of that first 6kb chunk of blank memory.

This little modification ensures the bootloader will run first when the chip is
powered,and the pinchange interrupt is necessary for V-USB on the device to function
in the bootloader.But wait - the user program needs to be able to use the V-USB to
talk over USB as well! Embedded Creations came up with a really neat solution for
that in their USBaspLoader-tiny85 project:
Whenever the bootloader is running a special part of memory contains 0xB007 -whenever
the pin change interrupt handler function is run inside of the bootloader, it checks
if those two bytes are there, and if not, it immediately jumps to the user program's
pinchange handler. This detect and jump behaviour is fast enough to not cause any
problems with the V-USB software, but does mean other programs using PCINT (pin
change interrupt) on the anuduino will find there's a slightly longer delay before
their function runs than there is on a raw chip with no bootloader.

For more information on the tricks micronucleus uses to add a bootloader on a chip with no
built in bootloader features, check out embedded-creations `USBaspLoader-tiny85 site
<http://embedded-creations.com/projects/attiny85-usb-bootloader-overview/>`_


At what clock speed and voltage level does the circuit work?
------------------------------------------------------------

It uses the high speed PLL at 16MHz.The internal PLL of Attiny85
generates a clock frequency that is 8x multiplied from a source input.
By default, the PLL uses the output of the  internal, 8.0 MHz RC
oscillator as source and the safe voltage is 3.8V or more for this
speed. 16.0 Mhz is more useful with existing  arduino libraries.
Also if you Run the attiny85 at < 4V you might even brick it. That
puts the chip out of specifications and the results are unpredictable,
sometimes the bootloader  will overwrite bits of itself and brick the
device requiring a high voltage serial programmer (or regular ISP
programmer if you didn't disable the reset pin) to recover.Hence it's
suggested to use 5V supply.

What if my code is more than 6K?
--------------------------------

If you are uploading your sketch using Digispark integrated
Arduino IDE ,before uploading if you compile the code you will get an
idea of how much memory does your code need.So before uploading its a
good habit to first compile your code.In case it's more than 6kb it's
likely to overwrite your bootloader.In which case you have to reflash
the bootloader using ISP programmer.But you can reupload the bootloader
on your chip  only if your reset pin is disabled as I/O (reset HIGH).In
case your reset is enabled as I/O you will need HVSP (High volt serial
programmer) to reconfigure your chip to be programmed with ISP programmer.
Tersely ,it's a matter of fuse settings (specifically the RESET bit of
hfuse) of your chip.

Can I use it in other OS ?
--------------------------

It can be used on GNU/Linux, Aakash tablet running on Ubuntu-12.10 ARM
version,and various others. This tutorial is dispositioned more towards GNU/Linux users.

What all can it do ?
--------------------

It can be integrated with number of sensors (IR, proxomity, temperature),
bluetooth module,as a multimeter etc.

How serial communication occurs ?
---------------------------------

The anuduino does not have a hardware serial port nor a hardware serial to
USB converter. `V-USB <http://www.obdev.at/products/vusb/index.html>`_ is
a software-only implementation of a low-speed USB device for Atmel’s AVR
microcontrollers, making it possible to build USB hardware with almost any
AVR microcontroller, not requiring any additional chip for serial conversion.
Bluebie wrote the micronucelus bootloader which uses the V-USB project and
renders anuduino to be used as usb development board without need of any additional chip.

Whats is cdc232.hex ?
---------------------

cdc232 is a version of `this <http://www.recursion.jp/avrcdc/cdc-232.html>`_
project, Bluebie, the maker of micronucleus included this in the micronucleus
repository for people who might want it - basically it makes a anuduino into
a cheap USB to serial converter.It's just like any other sketch or hex file
and will be overwritten if you upload any other sketch say Blink.hex.

**If you upload sketches with DigiUSB libraries it detects as USB-HID(Human Interface Device)?**

It's ok if the anuduino doesn't detect as ttyACM device ,in general if a
device detects as tty device it means it is a USB-serial device.But anuduino
in not a USB-serial device ,it does not provide USB-serial interface. So when
you plug your anuduino ,the serial port tab of digispark integrated arduino
IDE will be greyed out.(link to the IDE is given below under the heading pre-requisite packages).

DigiUSB - Debugging and HID communication library
On the computer side you can use the included command line tools in the
DigiUSB Programs folder available in the Integrated IDE:
digiusb - this program is like the Arduino **serial monitor**, allowing
you to send and receive messages to/from a Digispark running DigiUSB

 .. image:: ../images/usbhid.png
    :width: 100%

If you upload a sketch with digiusb libraries then you can see it as HID device , do ::

  ls /dev/usb/hiddev0
