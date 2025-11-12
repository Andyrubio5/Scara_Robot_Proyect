# Scara_Robot_Project
## Advanced Embedded System Project

### Collaborators
    Andrea Zarahi Rubio Quezada | A01645257
    Fatima Alvarez Nuño | A01645815
    Gustavo Alexander Nuño Corvera | A01644775

---

## Project Overview
This project consists of implementing a SCARA-type robotic arm controlled by hand movements detected by a camera or by default commands. The captured movements are processed and transmitted to a microcontroller (ESP32), which executes the robot's motion in real time.

The system was originally developed in bare-metal, and now it is being migrated to FreeRTOS to ensure real-time scheduling, modularity, and fail-safe operation.

---

## Objectives
- Develop a SCARA robot prototype capable of replicating human hand movements and default trajectories.  
- Integrate computer vision for gesture and motion detection.  
- Implement a control loop for robotic joint positioning.  
- Migrate firmware from bare-metal to FreeRTOS using tasks, semaphores, and queues.  
- Guarantee real-time response and safe operation under multitasking.  
- Design a precise and modular robotic platform for medical training and microsurgical applications.  

---

## System Components

### Camera & Vision System
- Detects the operator's hand position or gestures.  
- Converts pixel coordinates to workspace coordinates.  
- Sends target positions to the microcontroller via Wi-Fi TCP communication.  

### Microcontroller Unit (ESP32)
- Runs FreeRTOS with multiple tasks:  
  - Motion control loop  
  - Communication task  
  - Safety task  
- Generates PWM or step/direction signals for DC or stepper motors.  

### SCARA Mechanical Structure
- Two-link arm with horizontal motion.  
- Designed for fast and precise movements.  

---

## Tools & Development Environment

### Hardware

#### Core Components
- **Raspberry Pi 3 Model B+**
  - CPU: Broadcom BCM2837B0, quad-core ARM Cortex-A53 @ 1.4 GHz  
  - Connectivity: Wi-Fi 2.4/5 GHz, Bluetooth 4.2, Ethernet  
  - Interfaces: GPIO, CSI (camera), I2C, UART, SPI, USB  
  - Operating voltage: 5V / 2.5A  
  - Function: Captures camera input, runs YOLO detection, and sends coordinates via Wi-Fi to the ESP32.  

- **Raspberry Pi Camera Module Rev 1.3**
  - Resolution: 5 MP, supports 1080p30 video  
  - Interface: MIPI CSI port  
  - Function: Real-time image acquisition for motion and gesture detection.  

- **ESP32-WROOM-32**
  - Dual-core Xtensa LX6 @ 240 MHz  
  - Integrated Wi-Fi and Bluetooth  
  - Function: Executes control logic, processes received coordinates, and drives the SCARA motors.  
  - Runs FreeRTOS with multiple concurrent tasks.  

#### Actuation System
- **Motor Drivers**
  - Interface between ESP32 outputs and the motor power stage.  
  - Ensure current and voltage protection for precise movement.  

#### Mechanical Structure
- **SCARA Arm**
  - Two-link planar design with rotary joints.  
  - Constructed from lightweight aluminum or acrylic for stability and speed.  
  - Provides high precision for horizontal motion tasks.  

#### Additional Components
- **Power Supply:** 5V / 2.5A for Raspberry Pi, 12V for motor drivers and actuators.  
- **Breadboard and jump wires:** For prototyping and signal routing.  

---

### Software

#### Raspberry Pi (Vision & Processing)
- **Operating System:** Raspberry Pi OS Lite (64-bit)  
- **Programming Language:** Python 3  
- **Main Libraries:**
  - `ultralytics` – YOLOv8 for motion and gesture detection  
  - `opencv-python` – video capture and image preprocessing  
  - `numpy` – numerical operations  
  - `socket` – Wi-Fi communication with ESP32  
- **Development Environment:** Visual Studio Code (Remote SSH) or Thonny IDE  
- **Vision Model:** `yolov8n.pt` (lightweight YOLO model optimized for Raspberry Pi)  

#### ESP32 (Control & Execution)
- **Framework:** FreeRTOS (real-time task scheduling)  
- **Programming Language:** C / C++  
- **Development Environment:** Arduino IDE or ESP-IDF  
- **Main Libraries:**
  - `WiFi.h`  
  - `ArduinoJson.h`  
  - `FreeRTOS.h`  
- **Main Tasks:**
  - Communication task  
  - Motor control task  
  - Safety and monitoring task  
- **Communication Protocol:** Wi-Fi TCP (client-server)  
- **Motor Control:** PWM or step/direction output for servo or stepper motors  

#### General Tools
- **Version Control:** Git + GitHub  
- **Dependency Management:** `pip` (Python) and Arduino Library Manager  
- **Documentation & Presentation:** Markdown, Canva, and Notion  

---

## Application

### Medical Purpose
- The SCARA robot is designed for medical and surgical assistance, capable of performing precise movements such as suturing or controlled incisions.  
- Its goal is to support surgeons in tasks that require high stability, repeatability, and precision beyond natural hand control.  

### System Workflow
- The Raspberry Pi 3 B+ captures real-time video using the Raspberry Pi Camera Module Rev 1.3.  
- Through YOLOv8 (Ultralytics), the system detects and tracks the operator’s hand or specific surgical gestures.  
- Detected motion data (e.g., target coordinates and orientation) are transmitted to the ESP32 over Wi-Fi TCP sockets.  

### ESP32 Control Layer
- The ESP32 runs a FreeRTOS-based architecture, managing concurrent tasks for motion control, safety, and communication.  
- It interprets the received data and translates it into coordinated joint movements of the SCARA robotic arm.  
- The arm executes movements using PWM or step/direction control for its actuators, ensuring smooth and precise operation.  

### SCARA Robotic Arm
- Equipped with two rotary joints, the arm performs planar motion optimized for medical tasks.  
- The structure allows for precise and consistent trajectories, minimizing human error in delicate surgical procedures.  
- Its modular design makes it adaptable for training simulators or robot-assisted surgery prototypes.  

### Safety and Monitoring
- A dedicated safety task monitors the system’s status, ensuring stability, temperature control, and motor protection.  
- Fail-safe mechanisms stop movement in case of communication loss or unexpected sensor input.  

### Future Development
- Integrate force sensors or encoders for real-time feedback and haptic response.  
- Implement a machine learning model for gesture recognition and autonomous correction.  
- Extend to multi-arm coordination or teleoperation systems for remote surgical assistance.  

---
## Operating Modes

### 1) Surgical Presets (Parametric Replay)
Preprogrammed, parameterized surgical motions (e.g., suturing, linear/circular incision) that can be reused with new ranges and constraints.
- Examples:
  - Suture Line: `start_point`, `end_point`, `stitch_spacing`, `depth`, `passes`, `speed`.
  - Circular Incision: `center`, `radius`, `depth`, `speed`, `laps`.
- Guarantees:
  - Deterministic timing (fixed control/update rate).
  - Jerk-limited, smooth trajectories (minimum-jerk or quintic polynomials).
  - Hard/soft limits and virtual fixtures to prevent unsafe motion.

### 2) Vision-Guided Imitation (Mirror Mode)
The SCARA mirrors the surgeon’s hand motion tracked by YOLOv8 on the Raspberry Pi.
- Pipeline: Camera → YOLO → filtering → pixel-to-world transform → TCP packet → FreeRTOS control → inverse kinematics → motion.
- Stability:
  - Signal conditioning: EMA/Kalman filtering, deadband, and rate limiting.
  - Trajectory smoothing: cubic spline or minimum-jerk before sending setpoints to the controller.
  - Safety envelope: virtual fixtures and workspace limits enforced at the controller.

### 3) Teach & Replay (optional)
Record a trajectory demonstrated by the operator (via vision or jog control) and replay it with parametrization (scale, offset, speed).
- Use cases: repeatable training patterns, benchmarking, or quick prototyping of new procedures.

--- 
## Teamwork & Roles

### Software Role
Responsible: @nunocorverag  

### Hardware Role
Responsible: @Andyrubio5  

### DSP and Control Role
Responsible: @fatimaalvarez-creator  

### Management and Integration
Responsible:  
@fatimaalvarez-creator  
@Andyrubio5  
@nunocorverag  

---

## External Documents
This repository includes important documentation that complements the SCARA robot project:
- [Project Calendar](docs/Calendar/README.md)  
- [Expenses & Budget](docs/Expenses/README.md)  
- [Wiring](docs/Wiring/README.md)  
- [Datasheets](docs/Datasheets/README.md)  
- [Presentations](docs/Presentations/README.md)  

---

## References
- FreeRTOS. (n.d.). *FreeRTOS – Real Time Operating System*. https://www.freertos.org/  
- OpenCV. (n.d.). *OpenCV Documentation*. https://docs.opencv.org/  
- STMicroelectronics. (2025). *STM32H7 Nucleo-144 boards (UM2408 User Manual).*  
- Raspberry Pi Ltd. (2025). *Raspberry Pi 3 Model B+ product brief.* Raspberry Pi. https://datasheets.raspberrypi.com/rpi3/raspberry-pi-3-b-plus-product-brief.pdf
