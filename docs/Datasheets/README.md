# DataSheets and Documents

This directory contains all the datasheets and technical documentation of the main components used in the **SCARA Robot Project** running on **FreeRTOS**.  
The purpose of this section is to provide quick access to all relevant hardware and electronic references for development, debugging, and validation.

---

## Documents Included

### STM32H7 Nucleo-144 (UM2408)
- **File:** [datasheet-tm32h7-nucleo144.pdf](datasheet-tm32h7-nucleo144.pdf)  
- **Description:**  
  User manual of the STM32H7 Nucleo-144 development board used as a reference microcontroller platform for initial system design and task-based control validation.  
  Includes detailed information about pinouts, peripherals, debugging interfaces, and MCU specifications.

---

### RTOS with Microcontrollers
- **File:** [Hands-On-RTOS-with-Microcontrollers-Building-real-time-embedded-systems-using-FreeRTOS-STM32-MCUs.pdf](Hands-On-RTOS-with-Microcontrollers-Building-real-time-embedded-systems-using-FreeRTOS-STM32-MCUs.pdf)  
- **Description:**  
  A comprehensive guide for learning to design and implement real-time embedded systems using **FreeRTOS** on STM32 microcontrollers.  
  This reference was used to understand multitasking, scheduling, synchronization primitives, and communication mechanisms between tasks.

---

### Raspberry Pi 3 Model B+
- **File:** [raspberry-pi-3-b-plus-product-brief.pdf](raspberry-pi-3-b-plus-product-brief.pdf)  
- **Description:**  
  Technical brief of the **Raspberry Pi 3 Model B+**, used as the main vision and processing unit in the project.  
  Includes details about:
  - Broadcom BCM2837B0 CPU (Quad-core ARM Cortex-A53 @ 1.4 GHz)  
  - 1 GB LPDDR2 memory  
  - Dual-band 2.4/5 GHz Wi-Fi and Bluetooth 4.2/BLE  
  - CSI interface for camera module connection  
  - USB and GPIO interface support  
  - Power requirements and operating temperature range  

  This document serves as a reference for configuring the **vision subsystem**, ensuring compatibility between the camera module and the processing hardware.  
---

This centralized documentation ensures consistency and traceability across all project development stages.
