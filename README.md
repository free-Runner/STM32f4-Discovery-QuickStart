This project is based on jeremyherbert's stm32-templates, found at https://github.com/jeremyherbert/stm32-templates.

Forked from: https://github.com/prattmic/stm32f4-templates

This files here are only relevant to the stm32f4-discovery board and include the CMSIS library configured to be built along side main.c.
The goal is to provide a quickstart guide for the stm32f4 board on a Linux box.

Instructions:

Prerequisites:
arm-none-eabi-gcc, found here: https://launchpad.net/~terry.guo/+archive/gcc-arm-embedded
STLINK (discovery uses v2), found here: https://github.com/texane/stlink

Compile code:
Create main.c in src/
All header files should be placed in inc/
Run Makefile with make
main.bin, main.elf, main.hex should be created

Loading Code onto board:
Option 1:
Here, we'll run a GDB server and load the code from there
In STLINK, use the following command:

sudo ./st-util

This starts the STLINK utility to talk to the board.
In another window, run a gdb server and run the code:

arm−none−eabi−gdb ./main.elf
(gdb) target extended localhost:4242
(gdb) load
(gdb) continue

Option 2:
Here, we'll directly write a section of the memory
In STLINK, use the following command:

sudo ./st-flash write /path/to/main.bin 0x80000000

This will write the bin image in the correct place in memory to be executed by the board. This method allows us to read at any location as well with the read command:

sudo ./st-flash read main.bin 0x80000000 2048

The command is reading 2048 bytes from the beginning of the program.
