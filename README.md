# Smart Automatic Door System

![Status](https://img.shields.io/badge/Status-Completed-success)
![Hardware](https://img.shields.io/badge/Hardware-Electronic_Circuit-orange)
![Voltage](https://img.shields.io/badge/Voltage-12V_%2F_5V_%2F_3.3V-red)
![Course](https://img.shields.io/badge/Course-Electronic_Devices_and_Circuits-blue)

**Course:** Electronic Devices and Circuits (CE124.Q14)

**Institution:** University of Information Technology (UIT) - VNU-HCM

**Instructor:** Dr. Tran Quang Nguyen

## 📸 Final Product Showcase

Below are the images of the completed system, highlighting the circuit assembly and mechanical structure:

<div align="center">
  <img width="2048" height="1536" alt="image" src="https://github.com/user-attachments/assets/2e30c013-486f-4acd-89c4-63dba893672b" />

  <img width="2048" height="1536" alt="image" src="https://github.com/user-attachments/assets/cf816f0d-6245-458d-9640-94c6357d80dc" />

  <img width="2048" height="1536" alt="image" src="https://github.com/user-attachments/assets/4eb75b44-c244-41c4-ac3a-3a185391c3e2" />

</div>

*Figure 1: The complete system setup including the sensor unit, control circuit, and actuator mechanism.*

## 📖 Overview

This project focuses on the analysis and application of **Electronic Devices** to construct a **Smart Automatic Door System**.
Unlike purely software-based projects, this study emphasizes the **electrical characteristics**, **component specifications**, and **circuit design** required to drive a high-power DC motor using low-voltage logic control signals from the STM32 microcontroller.

## 🛠 Tech Stack & Methodology

* **Design Methodology:**
    * **Circuit Analysis:** Calculating current/voltage requirements for the Motor and Driver.
    * **Component Selection:** Choosing the H-Bridge driver based on power dissipation and peak current ratings.
* **Hardware Components:**
    * **Controller:** STM32F407VET6 (ARM Cortex-M4).
    * **Power Stage:** L298N Dual Full-Bridge Driver (Bipolar tech).
    * **Sensor:** HC-SR04 (Ultrasonic Transducer).
* **Tools:**
    * **Altium Designer / Proteus:** For circuit design and simulation.
    * **STM32CubeIDE:** For firmware implementation.

## ⚡ Component Specifications & Analysis

The system consists of three main stages with specific electrical parameters:

### 1. Control Stage (STM32F407VET6)
* **Operating Voltage:** $3.3V$ DC.
* **Clock Frequency:** $168 \text{ MHz}$.
* **GPIO Output Current:** Max $25 \text{ mA}$ (Sufficient to drive L298N Logic Inputs).

### 2. Power Driver Stage (L298N H-Bridge)
* **Device Type:** Dual Full-Bridge Driver (Transistor Logic).
* **Supply Voltage ($V_s$):** Supports up to $46V$ (We utilize $12V$).
* **Peak Output Current ($I_o$):** $2A$ per channel.
* **Logic High Voltage ($V_{IH}$):** $2.3V \le V_{in} \le V_{ss}$ (Compatible with STM32 3.3V logic).
* **Power Dissipation:** Heatsink required for currents $> 1A$.

### 3. Sensor Stage (HC-SR04)
* **Operating Voltage:** $5V$ DC.
* **Operating Current:** $15 \text{ mA}$.
* **Frequency:** $40 \text{ kHz}$.
* **Range:** $2 \text{ cm} - 400 \text{ cm}$.

## 📊 System Operation Logic

The circuit operates by switching the transistor states within the L298N H-Bridge to control current flow direction through the DC Motor.

| Condition | Sensor Distance ($d$) | MCU Signal (PB0 / PB1) | H-Bridge State | Motor Action |
| :--- | :--- | :--- | :--- | :--- |
| **User Approaching** | $d < 15 \text{ cm}$ | `HIGH` / `LOW` | Q1, Q4 ON | **Forward (Open)** |
| **Holding Open** | (Delay 3s) | `LOW` / `LOW` | All OFF | **Stop (Coast)** |
| **User Away** | $d \ge 15 \text{ cm}$ | `LOW` / `HIGH` | Q2, Q3 ON | **Reverse (Close)** |

## ⚙️ Installation & Setup

1.  **Clone the Repository:**
    ```bash
    git clone https://github.com/NguyenDinhNhatNguyen/Auto-Door
    ```
2.  **Hardware Wiring:**
    * Connect **12V Source** to L298N $V_{CC}$ and **GND** to common ground.
    * Connect **STM32 PB0, PB1** to L298N **IN1, IN2**.
    * Connect **STM32 PA1, PA6** to Sensor **Trig, Echo**.
    * **Caution:** Ensure common GND between 12V and 5V/3.3V sources.
3.  **Flash Firmware:**
    * Load the `.elf` file using STM32CubeIDE or ST-Link Utility.

## 👥 Contributors & Roles 

| Student Name | ID | Role | Responsibilities |
| :--- | :--- | :--- | :--- |
| **Le Hung Phat** | 23521139 | **System Arch** | System integration, Firmware logic, Schematic design. |
| **Nguyen Thanh Hieu** | 23520486 | **Power Electronics Eng.** | L298N & Motor analysis, Power calculations, Thermal analysis. |
| **Tran Quang Nhat** | 23521102 | **Control Circuit Eng.** | STM32 interface design, Simulation (Proteus), Wiring. |
| **Nguyen Dinh Nhat Nguyen** | 23521043 | **Sensor & Mech. Eng.** | HC-SR04 signal analysis, Mechanical build, Calibration. |
| **Ngo Tien Dat** | 23520254 | **QA & Technical Writer** | Testing & Measurements, Debugging |
---
*Ho Chi Minh City, January 2026*
