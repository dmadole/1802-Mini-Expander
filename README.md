# 1802-Mini-Expander-RTC
This is the memory and port expander plus real-time clock card for the [1802/Mini](https://github.com/dmadole/1802-Mini) system. It supports the following features:

### Memory Expansion

* 32K added ROM or RAM
* Can be addressed in either upper or lower 32K block
* Can be split on any power of 2 size from the top or bottom of the block
* Splitting the block allows mixed ROM and RAM in the same 32K block
* Expansion memory can be enabled or disabled under software control
* Can be set to be enabled or disabled be default at system reset

The software control can be used to implement bank switching, such a 32K ROM that includes diagnostics run at boot time but is then replaced with RAM except for the last 2K or 4K which has BIOS. Or you could have a system that can start either a Riley “Disk-less ROM” with 32K RAM/32K ROM, or a Elf/OS system with 60K RAM/2K ROM under control of a software menu.

### Real Time Clock

* Keeps month, day, year, hour, minute, second time and date
* Corrects for leap years
* Can provide a periodic interrupt at 64 Hz or once per second, minute, or hour
* Can also provide a pollable signal on an EF line at the same rates
* Uses a replaceable BR1225 coin cell battery
* 1.3uA standby current gives approximately 5 years battery life
* Uses one I/O port 1-7 which is two-level group addressable

I have written a loadable driver that presents the “standard” interface to Elf/OS 4 to enable date and time. The same code could be put into ROM if needed.

### Port Expander

* Implements low 4 bits of the Microboard group scheme
* Written group select value can be read back also
* Implements a “group 0” which is automatically selected at reset
* Total of 5 groups gives 35 maximum I/O ports (5 groups of 7)
* Allows for high 4 bits to be implemented on another card
* Uses one I/O port 1-7

Gerber files for the PCBs and PDF schematics can be found in [Releases](https://github.com/dmadole/1802-Mini-Expander-RTC/releases).

BOMS and any applicable errata or other notes can be found in [notes](https://github.com/dmadole/1802-Mini-Expander-RTC/tree/main/notes).

For availability of kits and bare PCBs please see http://madole.net/1802/mini/kits

![1802/Mini Expander RTC Front](https://github.com/dmadole/1802-Mini-Expander-RTC/blob/main/photos/1802-Mini-Expander-RTC-Rev-A-Assembled-Front.jpg)
 
