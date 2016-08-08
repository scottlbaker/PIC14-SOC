
## Summary

This project is an SOC (System on a Chip) coded in VHDL and implemented for the Lattice iCE40-hx8k dev board. The SOC contains the following components: PIC-14 CPU + UART + Timer + I/O Ports

## Required Hardware

* Lattice iCE40-hx8k dev board (can be ordered online at www.latticesemi.com)
* USB-to-Serial 3.3V adapter (can be ordered from eBay)
* misc USB cables and wires for connecting the USB-to-Serial adapter

NOTE: Make sure the USB-to-serial adapter is a 3.3V version. Some adapters have 5V interface signals which could damage your iCE40-hx8k dev board.

## Tools

* IceCube2 (from Lattice Semiconductor) was used for synthesis and FPGA Routing.
* Icestorm (https:/github.com/cliffordwolf/icestorm) was used for programming.


## Build Flow

I used the Lattice IceCube2 software to generate the SOC_bitmap.bin programming file and then I used this command line "iceprog SOC_bitmap.bin" the program the iCE40-hx8k dev board over the USB cable (iceprog is part of the icestorm tool suite).

## Console Interface

I used the minicom program (on Ubuntu Linux) as a console to communicate with the PIC-14 SOC over the USB-to-Serial connection. Configure minicom using the command line "minicom -s" to configure the serial port for ttyUSB0 and turn of the hardware handshaking. There are probably other alternatives to minicom. Any ANSI terminal-emulator program should work for this application.

## Pinout

The iCE40 pins are defined as follows:
```
UART_RXD   G1 -pullup yes
UART_TXD   G2
PORTA[0]   B5
PORTA[1]   B4
PORTA[2]   A2
PORTA[3]   A1
PORTA[4]   C5
PORTA[5]   C4
PORTA[6]   B3
PORTA[7]   C3
RESET      N3 -pullup yes
CLK        J3 -pullup yes
```

## Register Map

The register map of this SOC is as follows:
```
INDF    00h     INDF    80h     INDF    100h     INDF    180h
TMR0    01h     OPT     81h     TMR0    101h     OPT     181h
PCL     02h     PCL     82h     PCL     102h     PCL     182h
STATUS  03h     STATUS  83h     STATUS  103h     STATUS  183h
FSR     04h     FSR     84h     FSR     104h     FSR     184h
PORTA   05h     TRISA   85h
PCLATH  0Ah     PCLATH  8Ah     PCLATH  10Ah     PCLATH  18Ah
INTCON  0Bh     INTCON  8Bh     INTCON  10Bh     INTCON  18Bh
PIR1    0Ch     PIE1    8C
TMR2    11h
T2CON   12h     PR2     92h
RCSTA   18h     TXSTA   98h
TXREG   19h     SPBRG   99h
```

## PIC CPU Background Info

The PIC (Peripheral Interface Controller) is one of the most prolific and successful microcontroller designs of all time. It was developed in the early 1980's by General Instruments for use in their in-house designs.  In the late 1980's, General Instruments spun off Microchip, Inc. which continues to develop and support the PIC product line. The PIC's main differentiating feature is it's separate data and program memory buses.  This is know as a Harvard architecture, and it has the following advantages.  There is more memory bandwidth since both memories can be accessed simultaneously and instruction width is not tied to data width. There are many versions of the PIC, this on has has an 8-bit-wide data memory and a 14-bit-wide program memory and includes ports A,B,C and Timers 0, 1 and 2 (although on this dev board only Port A output pins are available).


## Contributors

* Scott L Baker - SOC design

## License

See the **LICENSE** file in this repository
