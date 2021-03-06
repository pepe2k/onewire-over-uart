# onewire-over-uart:
## Access Dallas 1-wire bus on your PC with simple and cheap hardware.

This project is based on Maxim's application note:
Using a UART to Implement a 1-Wire Bus Master

[http://www.maximintegrated.com/app-notes/index.mvp/id/214](http://www.maximintegrated.com/app-notes/index.mvp/id/214 "Using a UART to Implement a 1-Wire Bus Master")

***
### Hardware

The original version mentioned in Maxim's application note is shown as below.

![Schematics](docs/pp2od_tt.png "Original version")

Also a simplified version is available:

![Schematics](docs/pp2od_rd.png "Simplified version")

Resistors can vary from 200ohm to 20kohm. Transistors can be BJTs or MOSFETs.
The diode used in the simplified version should be fast and has a low forwarding voltage.
1N4148 is known to work.

A USB to UART converter is needed.
There are many USB to UART converters that have a TTL UART interface.
RS-232 UARTs should be avoided since its voltage is very high and can damage your device.
If you have to use one of such, insert a MAX232 or equivalent chip between the RS-232 port and
the circuits mentioned above properly.

Here are a few models that are tested. Many of these are prices under $5:

* SiLabs CP2102 USB to UART converters (shown below) are known to work.

    ![Photo](docs/cp2102.jpg "CP2102")

* Prolific PL2303 USB to UART converters (shown below) are also known to work,
    but most boards have problematic power output pins.
    Try to power your 1-wire device separately or strange things will happen.

    ![Photo](docs/pl2303.jpg "PL2303")

* FTDI FT232L USB to UART converters (shown below) are also known to work,
    but they are more expensive than the former two types.

    ![Photo](docs/ft232l.jpg "FT232L")

***
### Software

Type "make" to get "lsow" and "digitemp\_evil" compiled.

lsow is a tool that list devices on a onewire bus connected to a USB to UART converter.
Simply type something like "lsow /dev/ttyUSB0" and it will show device IDs found on the bus.

digitemp\_evil is a demonstration program that reads temperature values from DS18S20/DS18B20/DS1822
onewire digital temperature sensors. Type "digitemp\_evil /dev/ttyUSB0" and read IDs and values.
Sometimes after powering up DS18B20 will give something like 85°C, you will just need retry.

![Terminal Output](docs/dte.png "digitemp\_evil's output")
