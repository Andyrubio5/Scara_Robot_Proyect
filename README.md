# Scara_Robot_Proyect
## Advanced Embedded System Proyect 

### Colaborators 
    Andrea Zarahi Rubio Quezada | A01645257
    Fatima Alvarez Nuño | A01645815
    Gustavo Alexander Nuño Cano | A01644775

## Proyect Overview 
This proyect cosists of implementig a SCARA-type robotic arm controlled by hand movements detected by a camera or by default commands. The captured movements are processed and trasmitted to a microcontroller (STM32H7), which executes the robot's motion in real time.

The system was originally developed in bare-metal, and now it is being migrated to FreeRTOS to ensure real-time scheduling, modularity, and fail-safe operation. 

## Objectives
- Develop a SCARA robot prototype capable of replicating human hand movements and default ones. 
- Integrate computer vision for gesture/motion detection.
- Implement a control loop for robotic joint positioning 
- Migrate firmware from bare-metal to FreeRTOS, using tasks, semaphores, and queues.
- Guarantee real-time response adn safe operation under multitasking.

## System Components 
### Camera & Vision System 
- Detects the operator's hand position or gestures
- Converts pixel coordinates to workspace coordinates.
- Sends target positions to the microcontroller via serial communication,.
### Microcontroller Unit (STM32H7 Nucleo-144)
- Runs FreeRTOS with multiple tasks:
    - Motion control loop 
    - Communication task
    - Safety task
- Generates PWM signals or step/direction for servos/steppers
### SCARA Mechanical Structure
- Two-link arm with horizontal motion
- Designed for fast and precise motions

## Tools & Development Enviroment
### Hardware
    - STM32H7 Nucleo-144 
    - DC Motors
    - Encoders
    - SCARA frame.
### Software
    - STM32CubeIDE + FreeRTOS
    -Git/GitHub for verision control

## Application

## Teamwork & Roles 
### Software Role:
Responsable:

Tasks:
### Hardware Role:
Responsable:

Tasks:
### DSP and Control Role:
Responsable:

Tasks:

## External Documents 
This repository includes importante documentation that complements the SCARA robot project:
- [Proyect Calendar](docs/Calendar/README.md)
- [Expenses & Budget](docs/Expenses/README.md)
- [Wiring](docs/Wiring/README.md)
- [Datasheet](docs/Datasheets/README.md)
- [Presentations](docs/Presentations/README.md)
- [Important](docs/Importants/README.md)

## References
- FreeRTOS. (s. f.). FreeRTOS – Real Time Operating System. https://www.freertos.org/

- OpenCV. (s. f.). OpenCV Documentation. https://docs.opencv.org/

- STMicroelectronics. (2025). STM32H7 Nucleo-144 boards (UM2408 User Manual).