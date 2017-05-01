# '''Specification Table''' 
The up up-to-date specification table
{| class = "wikitable"
|-
!width ="100"|
!width ="150"|BeagleBone Black 
(BBB)
!width = "150"|BeagleBone 
(Original)

!width ="100"|Arduino
!width ="100"|Raspberry Pi 2
Model B


|-
|Processor || AM3358 
ARM Cortex-A8
|| AM3358 
ARM Cortex-A8
|| ATmega328||BCM2836
ARM Cortex-A
|-

|Maximum Processor
speed
 ||1GHZ
|| 720MHZ
||16MHZ||900 MHZ
|-

|Analog Input
Pins
 || 7 12-bit
||  7 12-bit
|| 6 10-bit|| N/A
|-

|Digital I/O  Pins
 || 65 (3.3V)
||  65 (3.3V)
|| 14|| 40(3.3V)
|-

|Memory
||512MB DDR3 (800MHz x 16), 2GB ( 4GB on Rev C) on-board storage using eMMC, microSD card slot
||256MB DDR2 (400MHz x 16), microSD card slot.
|| 2KB (SRAM)|| 1GB LPDDR2
|-
|USB
 || HS USB 2.0 Client Port, LS/FS/HS USB 2.0 Host Port
||  miniUSB 2.0 client port, USB 2.0 host port
|| N/A|| 4xUSB2.0 Connector

|-
|Video Output
 || microHDMI, cape add-ons
|| cape add-ons
|| N/A|| HDMI (rev 1.3 & 1.4) 
|-
|Audio Output
 || microHDMI, cape add-ons
|| cape add-ons
|| N/A|| HDMI, Analog
|-
|Supported Interfaces
 || 4x UART, 8x PWM, LCD, GPMC, MMC1, 2x SPI, 2x I²C,  2xCAN Bus, 4 Timers
|| 4 x UART, 8x PWM, LCD, GPMC, MMC1, 2x SPI, 2x  I²C C, 2xCAN Bus, 4 Timers,
FTDI USB to Serial, JTAG via USB

||6x PWM, 2xSPI, 2xUART,  2x I²C C|| 1xSPI, 1xUART,  1x I²C C
|-
|Price
 || $49
|| $89
||$20|| $35
|-

|Operating Systems
 || Linux, Windows, Android, Cloud9 IDE on Node.js w/ BoneScript library
||Linux, Windows, Android, Cloud9 IDE on Node.js w/ BoneScript library
||Arduino Tools
Windows, Linux
||  Linux, Windows
|-
|Ethernet
 || 10/100
|| 10/100
||N/A|| 10/100
|-

|Input Voltage
 || 5v
|| 5v
||7-12v||5v
|-

|Dev IDE
 || Eclipse IDE, Visual Studio or others
|| Eclipse IDE, Visual Studio or others
||Eclipse IDE||Visual Studio IDE, Eclipse


|}

# '''Candidate Evaluation''' 
Based on the specification  table, one can see that Open
source Devices are quiet similar, which makes it not easy to choose which one
is the best candidate. However there are some differences between them in term
of performance, price, connectivity, customization, functionality and the
supported development tools. Based on
these information and the nature of the future project to be developed, in the
follows, we will discuss which device will be our best candidate for
the project.

Arduino has the lowest parameters such as Analog and
digital I/O, and processor speed which reduce its connectivity and
performance comparing to the three other competitors. These motivate us to dismiss
it from the beginning.

Raspberry Pi 2
provides 26 header pin, 4xUSB connector, a good processor speed but it doesn’t
provide an analog input facilities, which is one of our needed requirements for
the future project because of this requirement, Raspberry Pi 2 is also failed to be our
strongest candidate comparing to the two other competitors. 

BeagleBone Black (BBB) and BeagleBone (Original) are very similar
in functionality and performance. Both has 2x 46 pin headers which provide 92
possibilities of connection furthermore, they have 65 Digital GPIO pins and 7
Analog input pins.  However the minor differences
do exist in pricing, the maximum speed of processor and BeagleBone (original) doesn’t
provide MicroHDMI support, which make BeagleBone (Original) fail to be our strongest
candidate.

Most of the conditions are satisfied by BeagleBone
Black than any of the three others and in term of programming facilities, one
can program on BeagleBone Black using most of the popular and most used popular
IDE such as Eclipse and Visual studio.

Finally, will look BeagleBone Black as the strongest
candidate Open Hardware device for the fast prototyping.

For the rest of our study, we will use  '''Beaglebone Black Rev C'''. The specification of this Open Hardware product can be found in the table above.

# Beaglebone Black Licensing 
Consider  the information from Beaglebone website, there is no   license of  use BeagleBone Black and I have sent mail to  BeagleBone contact  person Gerald Colley  about licensing of this product design I said  there is

'''No license for this design'''. 

Some information on the terms of use of BeagleBone can be found  on the following website:

See &#x20;http://elinux.org/Beagleboard:BeagleBoneBlack


General info about Open Hardware license 

See also &#x20;&#x20;&#x20;https://en.wikipedia.org/wiki/TAPR_Open_Hardware_License

# Some References 

Raspberry Pi 2 Model B

https://cdn-shop.adafruit.com/pdfs/raspberrypi2modelb.pdf

Raspberry PI 2 Model and analogue input 

https://blogs.msdn.microsoft.com/cdndevs/2015/06/01/raspberry-pi-2-and-analog-input/

See also:

http://eu.mouser.com/new/seeedstudio/BeagleBone-black-vs-green/

Beaglebone Family

[Beaglebone Family](http://beagleboard.org/bone)
