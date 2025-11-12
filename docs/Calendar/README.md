# Project Calendar

## Overview
This section presents the official planning and progress tracking of the **SCARA Robot Project**, developed as part of the **Advanced Embedded Systems** course.  
The calendar provides a detailed overview of the project organization, including milestones, deadlines, deliverables, and progress made throughout the semester.

The purpose of this document is to maintain a structured development process that ensures coordination between hardware, software, and control teams.  
It also serves as evidence of the continuous evolution of the project — from conceptual design to implementation and testing.

---

## Semester Calendar
The **Semester Calendar (PDF)** is already available in this folder.  
It contains the full timeline of the project, including:
- Key academic dates and milestones.  
- Division of work into weekly and monthly goals.  
- Deliverables such as design documents, code implementations, and system tests.  
- Integration phases between the Raspberry Pi, ESP32 (FreeRTOS), and SCARA arm.  
- Review and evaluation checkpoints.  

This calendar allowed the team to maintain a clear timeline and to adapt efficiently to technical and academic requirements.

For collaboration and future modifications, the editable version of the calendar is available on Canva:
> [Edit on Canva](https://www.canva.com/design/DAGxS-sNyBE/1x9ZQzOAKz5DhQujfMkSXg/edit?utm_content=DAGxS-sNyBE&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton)

---

## Current Progress

As of the current phase of the semester, significant technical and structural progress has been achieved in the development of the **Medical SCARA Robotic Arm**.  
The team has worked on both the mechanical and electronic aspects of the system, ensuring that the hardware, vision, and control modules evolve coherently toward the project’s medical precision goals.

### 1. Physical Prototype
The physical version of the SCARA robot has been successfully assembled and tested.  
The structure integrates all motion axes and mechanical joints required for suturing and precise planar movements.  
Initial tests validated the arm’s range, stability, and alignment, allowing for performance adjustments before the next fabrication stage.

### 2. Design Modifications and Reprinting
After evaluating the initial prototype, several mechanical improvements were implemented:
- Adjustments to link dimensions and joint clearances for smoother rotation.  
- Reinforcement of the base to reduce vibration during fast or repetitive movements.  
- Optimization of motor mount geometry for improved alignment with the SCARA kinematics.  

All design corrections have been incorporated into updated CAD models, which are now ready for **reprinting and assembly of the second prototype version**.

### 3. Vision Module Initialization
The **computer vision subsystem** has been initiated using the **Raspberry Pi 3 Model B+** and the **Camera Module Rev 1.3**.  
The team successfully set up the environment to run **Python + OpenCV + YOLOv8**, enabling image capture and early-stage motion detection tests.  
This phase established the foundation for the **mirror mode**, where the SCARA will replicate the surgeon’s hand movements in real time.

### 4. Code Updates and Encoder Integration
The control code on the **ESP32 (FreeRTOS)** has been modified to integrate **rotary encoders** for precise feedback of joint positions.  
These updates improve trajectory accuracy and ensure stable closed-loop control.  
Additional refinements were made to the task management system, optimizing the communication and motor control loops for smoother motion execution.

### 5. Next Steps
The upcoming phase will focus on:
- Testing the reprinted mechanical structure.  
- Finalizing the vision–to–motion communication pipeline between the Raspberry Pi and the ESP32.  
- Tuning encoder-based PID parameters for precise positioning.  
- Integrating safety checks and defining workspace limits for surgical operation mode.

---

## Summary
The **Project Calendar** represents the foundation of time management and coordination for the SCARA Robot initiative.  
Through structured planning, continuous documentation, and team accountability, the project achieved:
- Consistent alignment between design, software development, and hardware implementation.  
- Effective time management that supported on-time delivery of prototypes and reports.  
- A clear trace of the decision-making and iteration process.  

This planning framework has been essential in maintaining an organized, goal-driven workflow for a medical-oriented robotic system requiring precision, safety, and reliability.
