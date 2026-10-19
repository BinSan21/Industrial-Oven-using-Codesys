
# Industrial Oven Control System Using CODESYS

### PLC-Based Industrial Oven Simulation with HMI Visualization

An Industrial Oven Control System developed using **CODESYS V3.5 SP21 Patch 3**. This project simulates an industrial drying oven using Programmable Logic Controller (PLC) programming in Structured Text (ST).

The system is designed to control and monitor oven temperature, manage heating and cooling, provide visual status indicators, and implement safety mechanisms to prevent overheating.

This project is **simulation-based only** and does not require physical PLC hardware.

---

## Project Overview

Industrial drying ovens are commonly used in manufacturing industries to remove moisture from metal fixtures after washing. However, some fixtures contain rubber O-rings that may be damaged when exposed to excessive temperatures.

This project demonstrates a simulated industrial oven capable of operating at user-defined temperatures while monitoring safety conditions.

The system includes an HMI where operators can set the desired temperature, monitor the simulated oven temperature, control oven power, and observe operating conditions through LED indicators.

The PLC program incorporates temperature simulation, process control, door-locking logic, alarm monitoring, and automatic shutdown protection.

---

## Development Environment

| Component | Description |
|-----------|-------------|
| Software | CODESYS V3.5 SP21 Patch 3 |
| PLC Device | CODESYS Control Win V3 x64 |
| Programming Language | Structured Text (ST) |
| Interface | CODESYS Visualization |
| Project Type | PLC Simulation |
| Hardware | No physical hardware required |

---

## Project Features

### 1. Temperature Control

- Allows operators to manually enter the desired oven temperature.
- Displays the current temperature using an HMI gauge.
- Simulates heating until the desired temperature is reached.
- Simulates cooling when the heating process stops.

### 2. Power Control

- Provides an ON/OFF rocker switch for controlling the oven.
- Includes an LED indicator displaying power status.

### 3. Status Indicators

The HMI includes LED indicators for:

- Oven power status
- Temperature ramping up
- Target temperature reached
- Door lock status
- Safe-to-open status

### 4. Safety System

- Monitors the simulated oven temperature.
- Activates an alarm when the temperature exceeds the configured O-ring safety limit.
- Triggers an automatic shutdown when the temperature reaches the critical safety threshold.
- Provides door-locking and safe-to-open indications based on oven conditions.

### 5. Alarm Management

- Includes an alarm table for displaying warnings.
- Supports alarm acknowledgment.
- Monitors excessive temperature conditions.
- Provides an automatic shutdown trip for critical overheating.

---

## Project Structure

The project follows a modular PLC programming approach using function blocks, global variables, and visualization components.

### CODESYS Device Structure

<h3>CODESYS Project Structure</h3>
<img src="screenshots/Screenshot%202025-11-15%20112314%281%29.png" alt="Project Structure" width="450">

The project contains:

- **PLC_PRG** — Main PLC program.
- **GVL_Oven** — Global variables for the HMI, temperature, and safety status.
- **FB_ProcessControl** — Manages the oven operating sequence.
- **FB_SafetyLogic** — Handles alarms, shutdown protection, and safety conditions.
- **FB_TemperatureSimulation** — Simulates oven heating and cooling.
- **Alarm Configuration** — Manages alarm conditions.
- **Visu_Oven** — Human Machine Interface for monitoring and control.
- **Task Configuration** — Organizes PLC execution tasks.

---

## HMI Design

The Human Machine Interface provides a visual representation of the industrial oven's operating conditions.

<h3>Industrial Oven HMI</h3>
<img src="screenshots/Screenshot%202025-11-15%20112446.png" alt="Industrial Oven HMI" width="900">

### HMI Components

| Component | Function |
|-----------|----------|
| Temperature Gauge | Displays the current simulated oven temperature |
| Temperature Spinner | Allows the operator to adjust the temperature setpoint |
| Rocker Switch | Controls oven power |
| Power LED | Indicates oven power status |
| Ramp Up LED | Indicates temperature is increasing |
| At Temp LED | Indicates the target temperature has been reached |
| Door Lock Indicator | Shows the door lock status |
| Safe to Open LED | Indicates when the oven has cooled sufficiently |
| Alarm Table | Displays temperature warnings and alarms |
| Alarm Acknowledgment Button | Allows the operator to acknowledge alarms |

---

## PLC Programming

The PLC control system is developed using Structured Text (ST).

### 1. Main Program — PLC_PRG

<h3>Main PLC Program</h3>
<img src="screenshots/Screenshot%202025-11-15%20112741.png" alt="PLC_PRG" width="900">

The main PLC program initializes and executes three function blocks:

- `FB_SafetyLogic`
- `FB_ProcessControl`
- `FB_TemperatureSimulation`

These function blocks are executed during the PLC scan cycle to manage the simulated industrial oven.

### 2. Global Variable List — GVL_Oven

<h3>Global Variable List</h3>
<img src="screenshots/Screenshot%202025-11-15%20112818.png" alt="GVL_Oven" width="900">

The Global Variable List stores the shared variables used by the control system, including:

- Oven power switch
- Temperature setpoint
- Current oven temperature
- O-ring temperature limit
- Heating command
- LED indicators
- Alarm conditions
- Door lock output
- Safety shutdown status

The variables allow the PLC program, function blocks, and HMI to communicate.

### 3. Process Control — FB_ProcessControl

<h3>Process Control Function Block</h3>
<img src="screenshots/Screenshot%202025-11-15%20112851.png" alt="FB_ProcessControl" width="900">

This function block manages the oven operating sequence using a state machine.

The operating states include:

- **Off** — Oven is switched off.
- **Idle** — Oven is waiting for operation.
- **Ramping** — Oven temperature increases toward the target.
- **At Temperature** — Oven has reached the desired temperature and performs the timed drying process.
- **Cooling** — Heating is disabled and the oven temperature decreases.

The function block also controls heating commands and status indicators.

### 4. Safety Logic — FB_SafetyLogic

<h3>Safety Logic Function Block</h3>
<img src="screenshots/Screenshot%202025-11-15%20112908.png" alt="FB_SafetyLogic" width="900">

This function block monitors temperature conditions to protect the oven and processed fixtures.

The safety functions include:

- Monitoring the O-ring temperature limit.
- Activating an alarm when the temperature exceeds the limit.
- Handling alarm acknowledgment.
- Triggering an automatic shutdown at the critical threshold.
- Controlling safety-related indicators and door status.

The configured example O-ring safety limit is **150°F**.

The critical shutdown threshold is **160°F**, which is 10°F above the configured O-ring limit.

### 5. Temperature Simulation — FB_TemperatureSimulation

<h3>Temperature Simulation Function Block</h3>
<img src="screenshots/Screenshot%202025-11-15%20112921.png" alt="FB_TemperatureSimulation" width="900">

This function block simulates oven temperature changes without requiring a physical temperature sensor or heating element.

The simulation uses the following parameters:

| Parameter | Value |
|-----------|-------|
| Heating Rate | 0.2°F per execution cycle |
| Cooling Rate | 0.1°F per execution cycle |
| Ambient Temperature | 75°F |

**Heating:** When the heating command is active, the simulated temperature gradually increases.

**Cooling:** When the heating command is inactive, the simulated temperature gradually decreases toward ambient temperature.

A lower temperature boundary prevents the simulated oven temperature from decreasing below the configured ambient temperature.

These are simulation parameters rather than calibrated real-world heating and cooling rates.

---

## System Operation

The simulated oven follows this general operating sequence:

1. The operator enters the desired temperature using the HMI.
2. The operator activates the oven using the power switch.
3. The system enables the simulated oven operation and applies door safety logic.
4. The temperature simulation increases the displayed oven temperature.
5. The ramp-up indicator shows that the oven is heating.
6. Once the target temperature is reached, the at-temperature indicator activates.
7. The process controller manages the drying duration.
8. The oven enters the cooling stage after the timed process.
9. The safe-to-open indicator is activated when the corresponding safety conditions are satisfied.
10. If an overtemperature condition occurs, the alarm system responds and the critical shutdown logic protects the simulated oven.

---

## How to Run the Project

### Requirements

- CODESYS V3.5 SP21 Patch 3
- Windows operating system
- Compatible CODESYS simulation environment or Control Win runtime

### Instructions

1. Download `Industrial_Oven.project` from this repository.
2. Open CODESYS V3.5 SP21 Patch 3.
3. Select **File → Open Project**.
4. Locate and open the downloaded project.
5. Verify the PLC device and project configuration.
6. Select **Build → Build** and check for compilation errors.
7. Enable simulation mode through **Online → Simulation**, or connect to a configured CODESYS Control Win runtime.
8. Select **Online → Login**.
9. Start the PLC application.
10. Open the `Visu_Oven` visualization.
11. Set the desired temperature and operate the simulated oven.

---

## Testing

The application was tested as part of the BCA153 Industrial Oven final project.

The documented testing focused on:

- Operator temperature input
- Temperature ramp-up indication
- Target temperature indication
- Oven power control
- Alarm table warnings
- Overtemperature monitoring
- Safe-to-open and door lock indications

The project documentation reports that the required HMI controls, warning indications, and simulated operating functions were demonstrated.

---

## Project Limitations

- The project is designed for simulation only.
- No physical heating element, temperature sensor, or PLC hardware is connected.
- Temperature changes are generated through software.
- Heating and cooling rates do not represent a calibrated industrial oven.
- Real-world industrial operation would require independent, validated safety systems.

---

## Academic Information

**Project Title:** Industrial Oven Control System

**Course:** BCA153 — Computer Applications in the Industry

**Institution:** Mindanao State University – Iligan Institute of Technology (MSU-IIT)

**College:** College of Computer Studies

**Department:** Department of Computer Applications

### Project Developers

- Binyusoph P. Sansarona
- KJ C. Villanueva

---

## Conclusion

The Industrial Oven Control System demonstrates how PLC programming and HMI visualization can be integrated to simulate an automated industrial process.

Using CODESYS V3.5 SP21 Patch 3, the project combines structured programming, temperature simulation, process control, alarm monitoring, and safety logic into a single industrial automation application.

The project serves as an educational example of PLC-based control systems and industrial process simulation.

---

**Developed using CODESYS V3.5 SP21 Patch 3 | Industrial Automation Simulation**
