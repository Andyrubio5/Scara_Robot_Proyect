# Wiring & Pinout – SCARA Robot

## Overview
This directory contains the **wiring diagrams**, **pin mappings**, and **hardware schematics** used in the **SCARA Robot Project** running under **FreeRTOS**.  
The goal of this documentation is to clearly describe all physical connections between the microcontroller, motors, sensors, encoders, and peripheral devices involved in the system.

Each diagram helps ensure reproducibility, simplifies debugging, and allows future improvements or expansions to be implemented safely.

---

## Included Documents
- **SCARA_Main_Wiring.pdf** – General wiring schematic of the full robotic system.  
- **ESP32_Pinout_Diagram.pdf** – Specific pin mapping for motor control, encoders, and communication interfaces.  
- **Power_Distribution.pdf** – Shows regulated voltage lines for logic (5V, 3.3V) and power (12V) systems.  
- **Communication_Interface.pdf** – Illustrates Wi-Fi TCP communication between Raspberry Pi and ESP32 modules.

All diagrams are included in this directory and have been validated against the physical connections used in the prototype.

---

## Main Components

### Microcontroller – ESP32-WROOM-32
- **Core:** Dual-core Xtensa LX6 @ 240 MHz  
- **Framework:** FreeRTOS (task-based control and scheduling)  
- **Power:** 3.3V logic  
- **Primary Functions:**
  - Generates PWM and step/direction signals for the DC or stepper motors.  
  - Handles serial communication and encoder readings.  
  - Executes safety and control tasks concurrently.  

**Pin Assignments (control side):**
| Function | GPIO | Notes |
|-----------|------|-------|
| Motor 1 PWM / Step | GPIO 18 | Base joint control |
| Motor 2 PWM / Step | GPIO 19 | Arm joint control |
| Motor Enable | GPIO 21 | Active LOW |
| Encoder 1 A | GPIO 32 | Quadrature input |
| Encoder 1 B | GPIO 33 | Quadrature input |
| Encoder 2 A | GPIO 25 | Quadrature input |
| Encoder 2 B | GPIO 26 | Quadrature input |
| Safety/E-stop | GPIO 4 | External interrupt |
| Communication TX/RX | GPIO 1 / GPIO 3 | UART (debug) |
| Wi-Fi TCP | Internal | Wireless link with Raspberry Pi |

---

### Raspberry Pi 3 Model B+
- **Role:** Vision and motion detection unit.  
- **Interface Used:** CSI (Camera Serial Interface) for the Pi Camera Rev 1.3.  
- **Connection to ESP32:** Wi-Fi TCP socket communication.  
- **Power:** 5V / 2.5A regulated supply.  

**Relevant Pins (when applicable for GPIO use):**
| Function | Pin | Description |
|-----------|-----|-------------|
| 3.3V Power | Pin 1 | Logic reference |
| Ground | Pin 6 | Common ground with ESP32 |
| I2C SDA/SCL | Pin 3 / Pin 5 | Optional sensor interface |
| UART TX/RX | Pin 8 / Pin 10 | Debug or alternative serial link |
| CSI Interface | Dedicated ribbon | Camera Module Rev 1.3 |

---

### DC Motors / Stepper Motors
- **Type:** NEMA 17 stepper or 12V DC motors (depending on stage).  
- **Driver Board:** L298N / A4988 (prototype stages).  
- **Supply:** 12V for power stage, 5V logic reference.  
- **Control Interface:** Step/Direction or PWM from ESP32.  

**Driver Wiring (example A4988):**
| Signal | ESP32 GPIO | Description |
|---------|-------------|-------------|
| STEP | GPIO 18 / GPIO 19 | Pulse input per motor |
| DIR | GPIO 22 / GPIO 23 | Rotation direction |
| ENABLE | GPIO 21 | Common enable |
| VMOT | 12V | Motor power |
| GND | Shared | Common ground |

---

### Encoders
- **Type:** Incremental rotary encoders (two-channel quadrature).  
- **Purpose:** Joint angle feedback for real-time position monitoring.  
- **Interface:** Digital inputs to ESP32 using GPIO interrupts.  
- **Power:** 5V or 3.3V (depending on encoder model).  
- **Notes:** Filter capacitors and pull-up resistors are used to reduce noise.

---

### Power Distribution
| Component | Voltage | Source |
|------------|----------|--------|
| ESP32 | 5V (regulated to 3.3V) | Logic power rail |
| Raspberry Pi | 5V / 2.5A | Dedicated supply |
| Motors | 12V | External DC supply |
| Camera | 5V via Pi | CSI interface |
| Encoders / Sensors | 3.3V–5V | From logic regulator |

All grounds are connected in common to prevent floating references between modules.

---

## Notes on Safety and Wiring
- Always disconnect power before modifying wiring.  
- Ensure the **motor drivers** have proper heat dissipation.  
- The **common ground** between logic and power systems is required for correct PWM and encoder signal interpretation.  
- Add inline fuses or resettable PTCs for the 12V rail to prevent short circuits.  
- Verify encoder voltage compatibility before wiring to ESP32 inputs.  

---

## Purpose of This Documentation
This wiring reference ensures that anyone reproducing, testing, or expanding the SCARA Robot system can do so with a clear understanding of its electrical and logical connections.  
It also supports maintenance, safety analysis, and troubleshooting in both the laboratory and prototype stages.
