# C-UAS micro-ROS Gateway: STM32

This repository contains the STM32 firmware acting as the deterministic communication bridge for the Hardware-in-the-Loop (HIL) C-UAS tracking system. It operates as a micro-ROS client, linking the high-level ROS 2 perception network to the low-level physical motor controllers.

---

## Core Architecture

- **micro-ROS Subscriber** — Runs an embedded `stm32_subscriber_node` that listens to the `/anti_uav/joint_command` topic, receiving `sensor_msgs/msg/JointState` payloads.
- **RTOS Integration** — Built on FreeRTOS, utilizing an independent `UART_Task` thread and OS thread flags for deterministic, non-blocking execution.
- **High-Speed Hardware Offloading** — Extracts targeted `pan_velocity` and `tilt_velocity` vectors and utilizes Direct Memory Access (DMA) to transmit the joint targets over UART (`huart1`) to the primary motor execution board.

---

## Build Instructions

This project is configured for **STM32CubeIDE**.

1. Import the project into your STM32CubeIDE workspace.
2. Build the project (Debug/Release).
3. Flash to the target STM32 board via ST-LINK.
