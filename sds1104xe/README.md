# Siglent SDS 1104X-E hardware information

![UART](pictures/board.jpg)

## Block diagram

We drew a [block diagram](block_diagram/block.pdf) of the scope

## Development interfaces

![UART](pictures/interfaces.jpg)

### JTAG

JTAG is available on J10 below the Zynq. It is directly compatible with the Digilent HS2.


### UART

UART is available on J11 next to the Zynq and the JTAG connector.


### Selecting between NAND and JTAG boot mode

J1 can be populated with a Jumper to select between NAND and JTAG boot. To use the Jumper the strapping resistor R70 needs to be moved to position R71. Moving it to R74 should select JTAG booting all the time without using the jumper. Should you lose the resistor: It's a 20K 0402 resistor. Tolerances don't matter.
