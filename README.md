# STM32_Microcontroller_Custom_Bootloader
##  About  
This repository contains bare-metal firmware for the STM32F446RE Cortex-M4 microcontroller, developed using GCC for ARM and the STM32 HAL library. The main objective of the project is to implement a bootloader capable of performing firmware updates over UART.
 

---

##  Features  
- Bootloader startup on MCU reset  
- Hardware initialization (HAL, GPIO, UART, CRC, Clock)  
- User-button based bootloader entry  
- UART communication with host for firmware update  
- Jump to user application if no update is requested  
- Support for multiple bootloader commands  

---

##  Hardware & Tools  
- **MCU**: STM32F446RE (NUCLEO-STM32F446RE board used for testing)  
- **Debugger/Programmer**: ST-Link  
- **Communication Interface**: UART  

---

##  Bootloader Flow  
1. MCU Reset  
2. Peripheral Initialization (HAL, GPIO, UART, CRC, Clock)  
3. Check if **User Button** is pressed:  
   - **Yes** → Enter Bootloader mode, wait for commands over UART  
   - **No** → Jump to User Application  

---

##  Supported Bootloader Commands  

| Host Command            | Code  | Bootloader Reply                   | Notes |
|--------------------------|-------|------------------------------------|-------|
| **BL_GET_VER**           | 0x51  | Bootloader version (1 byte)        | Read bootloader version |
| **BL_GET_HELP**          | 0x52  | Supported command codes (10 bytes) | List supported commands |
| **BL_GET_CID**           | 0x53  | Chip ID (2 bytes)                  | MCU identification |
| **BL_GET_RDP_STATUS**    | 0x54  | Flash read protection (1 byte)     | Read protection level |
| **BL_GO_TO_ADDR**        | 0x55  | Success/Error (1 byte)             | Jump to given address |
| **BL_FLASH_ERASE**       | 0x56  | Success/Error (1 byte)             | Erase flash sectors |
| **BL_MEM_WRITE**         | 0x57  | Success/Error (1 byte)             | Write data to memory |
| **BL_EN_RW_PROTECT**     | 0x58  | Success/Error (1 byte)             | Enable R/W protection |
| **BL_DIS_RW_PROTECT**    | 0x5C  | Success/Error (1 byte)             | Disable R/W protection |
| **BL_READ_SECTOR_STATUS**| 0x5A  | Sector status (2 bytes)            | Read protection status |

---
