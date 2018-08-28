[![Build Status](https://ci.appveyor.com/api/projects/status/rigvo8jwvgaxcbtp?svg=true)](https://ci.appveyor.com/project/RyanHope/hondaecu)

## Software

### Windows

HondaECU for Windows requires the libusbK driver. Download [Zadig](https://zadig.akeo.ie/) and use it to install the libusbK driver. There is a usage guide on the Zadig website if you need help using it. Once libusbK is installed for your FTDI device, download the latest release of HondaECU.exe.

#### Usage

```
HondaECU.exe --help
usage: HondaECU.exe [-h] [--checksum CHECKSUM] [--rom-size ROM_SIZE]
                   [--fix-checksum] [--debug]
                   {read,write,recover,validate_checksum,fix_checksum} binfile

positional arguments:
  {read,write,recover,validate_checksum,fix_checksum}
                        ECU mode
  binfile               name of bin to read or write

optional arguments:
  -h, --help            show this help message and exit
  --checksum CHECKSUM   hex location of checksum in ECU bin (default: 0x3fff8)
  --rom-size ROM_SIZE   size of ECU bin in kilobytes (default: 256)
  --fix-checksum        fix checksum before write/recover (default: False)

debugging options:
  --debug               turn on debugging output (default: False)
```

## Hardware

The easiest way to talk to the ECU via the k-line is a USB to serial (TTL) converter,
and a serial to k-line converter. This code assumes you are using a FTDI based USB to
serial converter though others may work. I used a FTDI Friend from [Adafruit!](https://www.adafruit.com/product/284).
For the serial to k-line converter I used the schematic below since it contained no
special ICs, just common transistors and R/C components that I had laying around the house.

A note about the circuit below, while the PL2303 is a perfectly good USB to serial converter, it does not support bit banging and is not recommended. If you do have one of these converters you will need to use one of the control lines for the init sequence and that complicates things. Just get yourself a FTDI chip, they are cheap.

![kline_interface_1](http://pinoutguide.com/images/upload/pinout_117944425_image.png)

A much nicer looking k-line to serial converter that I plan on implementing next is
this one that uses one that uses optocouplers to keep the bike power isolated from
your electronics.

![kline_interface_2](http://projects.gonzos.net/wp-content/uploads/2017/04/CTX-kline-interface-1024x514.png)


### Bench Harness

If you make a bench harness to work with your ECU you will need a 2.5 amp power supply. The ECU will power-up with a 2.0 amp power supply but transfer rates will be slow and you will get CRC errors.

## Tuning Software

* http://www.tunerpro.net
* http://www.romraider.com
* https://www.evc.de/en/product/ols/software


## General Resources

* http://forum.pgmfi.org/index.php
* http://ecuhacking.activeboard.com
* http://www.motorsport-brix.de
* http://projects.gonzos.net/ctx-obd
* http://opengarages.org/handbook/ebook


## Donation

If you found this project useful, please consider donating.

[![paypal](https://www.paypalobjects.com/en_US/i/btn/btn_donateCC_LG.gif)](https://www.paypal.com/cgi-bin/webscr?cmd=_s-xclick&hosted_button_id=XL3H864LE567E)
