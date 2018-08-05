# Siglent SDS 1202X-E hardware information

![UART](pictures/board.jpg)

## Block diagram

We drew a [block diagram](../sds1104xe/block_diagram/block.pdf) of the 4 channel version. The 2ch version looks exactly the same. Just with only one ADC and 2 frontends.

### JTAG

JTAG is available on J40 below the Zynq. It is directly compatible with the Digilent HS2.

![JTAG](pictures/jtag.jpg)

### UART

UART is available on J41 next to the PSU connector. Voltage levels are 3.3V

![UART](pictures/uart.jpg)

### Selecting between NAND and JTAG boot mode

J42 can be populated with a Jumper to select between NAND and JTAG boot. To use the Jumper R314 next to it must be removed as it is a 0 Ohm bridge which selects NAND boot by default

![Boot mode](pictures/bootmode.jpg)

### Turning on the board without an attached front-panel

Bridge Pin 3 on the front-panel flex connector to GND. Either to Pin 2 on the same connector which carries GND or to an RF shield or BNC connector


### PMIC PIC programming port

J43

    1   +5V
    2   GND
    3   MCLR
    4   CLK
    5   DATA

I'd be careful fucking around with this. I think I "bricked" my PIC or something else when trying to read the firmware


### Power sequencing

This is what the original app does.

On startup:

    #don't press the power button from the scope
    echo 922 > /sys/class/gpio/export
    echo out > /sys/class/gpio/gpio922/direction
    echo 0 > /sys/class/gpio/gpio922/value

    #inhibit PMIC from seeing pressed power button
    echo 924 > /sys/class/gpio/export
    echo out > /sys/class/gpio/gpio924/direction
    echo 1 > /sys/class/gpio/gpio924/value

On shutdown:

    #"push" button via software
    echo 1 > /sys/class/gpio/gpio922/value
    sync
    #let the PMIC see the pushed button to turn off
    echo 0 > /sys/class/gpio/gpio924/value
