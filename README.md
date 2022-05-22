# DWM SRAM Data Dive

This repository will store all of the information I can find as to how Dragon Warrior Monsters on the Gameboy Color stores its save data. An example sav file is provided and a screenshot of the below information highlighted is also available.

![image info](/example color.png)

## Found

Numbers given are the byte number.

16 : 1 byte of x-position
17 : 1 byte : y-position 

40 : 1 byte for text speed. 1-8 stored as 00 - 07 respectively

171 - 368 : part of checksum for sure


380-383 : 4 bytes of master name
389-391 : 3 bytes of current gold little endian
392-394 : 3 bytes of bank gold little endian
395-414 : 20 bytes of inventory
415-454 : 40 bytes of bank storage

456-458 : 3 bytes change order options. The number is the index of the monster stored in the save data. Starts counting from 0 with the monster at 507

497-498 : 2 bytes storing minutes and hours respectively

507 is the start of the first monster. Each monster is 149 bytes long. (2nd monster begins at 656, 3rd at 805 etc.) 4387 is the start of the second farm.



| **Location**            | **Information**                                                                                                                                                                                      |
|-------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|   507 : 1 byte          |   Bred/Farm/Party (00/01/02)                                                                                                                                                                         |
|   508-511 : 4 bytes     |   Monster name                                                                                                                                                                                       |
|   512-515 : 4 bytes     |   F0 F0 F0 F0 spacer                                                                                                                                                                                 |
|   516 - 518 : 3 bytes   |   Unknown                                                                                                                                                                                            |
|   519 - 522 : 4 bytes   |   OG Masters name                                                                                                                                                                                    |
|   523 - 526 : 4 bytes   |   F0 F0 F0 F0 spacer                                                                                                                                                                                 |
|   527 : 1 byte          |   Unknown                                                                                                                                                                                            |
|   528 - 529 : 2 bytes   |   Concatenated Parents ID                                                                                                                                                                            |
|   530 - 533 : 4 bytes   |   Dad’s Master                                                                                                                                                                                       |
|   534 - 537 : 4 bytes   |   F0 F0 F0 F0 spacer                                                                                                                                                                                 |
|   538 : 1 byte          |   Unknown                                                                                                                                                                                            |
|   539 - 542 : 4 bytes   |   Mom’s Master                                                                                                                                                                                       |
|   543 - 546 : 4 bytes   |   F0 F0 F0 F0 spacer                                                                                                                                                                                 |
|   547 : 1 byte          |   Unknown                                                                                                                                                                                            |
|   548 - 580 : 33 bytes  |   Skills monster has learned/can learn                                                                                                                                                               |
|   581 : 1 byte          |   Unknown                                                                                                                                                                                            |
|   582 : 1 byte          |   Current level                                                                                                                                                                                      |
|   583 : 1 byte          |   Max level                                                                                                                                                                                          |
|   584 - 586 : 3 bytes   |   Total Exp                                                                                                                                                                                          |
|   587 - 604 : 18 bytes  |   Stats (Current HP, Total HP, Current MP, Total MP, ATK, DEF, AGL, INT, WLD) Each gets 2 bytes incase it goes over 255. If over 255 it is little endian. 271 (0x010f) would be stored as 0x0F 0x01  |
|   605 : 1 byte          |   Breeding plus                                                                                                                                                                                      |
|   606 : 1 byte          |   00 is hatched. 01 is unhatched/egg form                                                                                                                                                            |
|   607-637 : 31 bytes    |   Unknown                                                                                                                                                                                            |
|   638-641 : 4 bytes     |   Dad’s Name                                                                                                                                                                                         |
|   642-645 : 4 bytes     |   F0 F0 F0 F0 spacer                                                                                                                                                                                 |
|   646 : 1 byte          |   Dad’s breeding plus                                                                                                                                                                                |
|   647-650 : 4 bytes     |   Mom’s Name                                                                                                                                                                                         |
|   651-654 : 4 bytes     |   F0 F0 F0 F0 spacer                                                                                                                                                                                 |
|   655: 1 byte           |   Mom’s breeding plus                                                                                                                                                                                |



## To-Do
Reverse Checksum to allow save editing
