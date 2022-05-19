# 1802/Mini Expander RTC Card Notes

Follow usual assembly practices, which I will not document here. I recommend installing the lowest-height components first (resistors, diodes, right-angle connectors), then the next higher (sockets), and so on.

Please review all jumper settings before trying to operate the board. In particular, a group select jumper must be installed for the board to work, in systems without group I/O capability, this should be on the ALL position.

## Diodes

Note that there are two different types of diodes on this board, 1N4148 switching diodes and 1N4622 zener diodes. Please be sure to install the correct diodes in the correct locations. The 1N4148 diodes are typically clear glass with orange internal contacts and install at D1-5, and the 1N4622 diodes are opaque black or gray and install at D6-7.

### Port Expander Configuration

The port expander uses a single I/O port which is set by the `EXP ADDR` jumpers by selecting the appropriately labeled address values. Valid values are 1-7, do not set all jumpers to 0.

The port expander implements the low four bits of this port and maps them to the `01`, `02`, `04`, and `08` expander bus pins as active-low. When none of the bits are set the `00` pin on the expander bus will be active; the register will be cleared to 00 when the system is reset.

### Real Time Clock Configuration

The RTC uses a single I/O port which is set by the `RTC ADDR` jumpers by selecting the appropriately labeled address values. Valid values are 1-7, do not set all jumpers to 0.

The RTC can be used with two-level I/O by installing a jumper appropriately on the `I/O GROUP` jumpers. For the port to always be present at its assigned address regardless of the port exapander register, set to `ALL`. To be present in the default group which will be selected at reset, set to `00`. Otherwise, jumper to the appropriate grounp.

## Memory Configuration

The expansion card adds 32K of RAM or EEPROM that can be mapped to either the upper or lower 32K, and can be split within the block so that either the upper or lower part of the block comes from the expansion card, and the other part comes from the on-processor memory. In memory maps with high ROM it is recommended that the ROM is on the processor card, as only that sock has the ability to temporarily map the ROM to 0000 at reset to allow automatic booting, and that RAM is used on the expansion card.

### Memory Type

The memory type is configured with jumpers on a 9-pin jumper block immediately adjacent to the memory socket as follows:

|        Type         |    Jumpers    |
|:-------------------:|:-------------:|
| 32K RAM (62256)     | 2/3, 5/6, 8/9 |

### Memory Size

The `SPLIT` jumpers determine the split point in the memory block between the on-processor memory and the expansion memory and can split the block at 256, 512, 1K, 2K, 4K, 8K, or 16K bytes, or the block can be not split at all. This allows, for example, to have part ROM and part RAM within the same memory bank.

To set the split size, install jumpers to the left starting at the labeled split point and for all higher split points. The jumpers for lower split points should be to the right side. For example, for a 2K split, set jumpers to the left for the `2K`, `4K`, `8K`, and `16K` positions, and to the right for the `256`, `512`, and `1K` positions.

To not split at all and have a single 32K block, set all positions to the right.

### Memory Configuration

The `CONFIG` jumpers determine where in the memory map the expansion memory resides.

The `LOW/HIG` jumper selects whether the expansion memory is in the 0000-7FFFF block (jumper to `LOW`) or the 8000-FFFF block (jumper to `HIG`).

The `TOP/BOT` jumper selected whether the split point is measured from the top (jumper to `TOP`) or the bottom (jumper to `BOT`) of the memory block. 

The `UND/OVR` jumper selects whether the expansion memory is "under" or "over" the split point. Jumpering to `UND` means the expansion memory will be at the beginning or end (depending on the `TOP/BOT` jumper) of memory in the block, with the on-processor memory on the other side of the split. Jumpering to `OVR` reverses this.

The `ENA/DIS` jumper determines whether the expansion memory will be enabled (jumper to `ENA`) or disabled (jumper to `DIS`) at reset. When disabled, the on-processor memory will occupy all of the memory block.

The following diagrams, based upon the example of a 2K split size, may help to clarify:

![Jumper Settings](https://github.com/dmadole/1802-Mini-Expander-RTC/raw/master/notes/1802-mini-memory-expander-configuration.png)
