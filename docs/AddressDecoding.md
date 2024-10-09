# Address Decoding

The address decoding logic is responsible for mapping the HW into the 6502 address space.

The memory map privides the specific details of what is map where.

## Using a EEPROM for address decoding

Assuming we only to support eight HW devices a 256 byte EEPROM can decode the addresses. 

A simple lookup table maps the top 8 address lines to 8 bits of data that are used for the chip select (CS) lines.

Initially it will look like this.

| Start | End | Use | A15 | A14 | A13 | A12 | A11 | A10 | A09 | A08 | CS0 (RAM) | CS1 (Serial) | CS2 (Future3) | CS3 (Future4) | CS4 (Future5) | CS5 (Future6) | CS6 (Future7)| CS7 (EEPROM) |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| 0000 | 7FFF | RAM | 0 | * | * | * | * | * | * | * | 1 | 0 | 0 | 0 | 0| 0 | 0 | 0 | 
| 8000 | 80FF | VIA | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0| 0 | 0 | 0 | 
| 8100 | 81FF | Serial | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 1 | 0 | 0| 0 | 0 | 0 | 
| 8200 | 82FF | Future3 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 1 | 0| 0 | 0 | 0 | 
| 8300 | 83FF | Future4 | 1 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 
| 8400 | 84FF | Future5 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 0| 1 | 0 | 0 | 
| 8500 | 85FF | Future6 | 1 | 0 | 0 | 0 | 0 | 1 | 0 | 1 | 0 | 0 | 0 | 0 | 0| 0 | 1 | 0 | 
| 8600 | 8FFF | EEPROM | 1 | * | * | * | * | 1 | 1 | * | 0 | 0 | 0 | 0 | 0| 0 | 0 | 1 | 

