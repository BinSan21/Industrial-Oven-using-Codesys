# Industrial Oven Control System — CODESYS Simulation

A **PLC-based industrial oven simulation** developed using **CODESYS V3.5 SP21 Patch 3**. The project models the temperature control and safety behavior of a drying oven used for metal fixtures after washing, including fixtures fitted with heat-sensitive rubber O-rings.

This is a **software simulation only**. No physical PLC, heater, door lock, or temperature sensor is required.

## Project Overview

The operator sets a target oven temperature and uses an HMI to monitor the heating process. The control program simulates temperature changes, manages the oven's operating states, displays status indicators, and responds to overtemperature conditions. The design emphasizes protecting the fixtures and their rubber O-rings from excessive heat.

**Development environment:** CODESYS V3.5 SP21 Patch 3  
**Programming language:** Structured Text (ST)  
**Target device shown in the project:** CODESYS Control Win V3 x64  
**Interface:** CODESYS Visualization (HMI)

## Features

- **Adjustable temperature setpoint:** Enter the target temperature in degrees Fahrenheit (°F) using the HMI spinner/input.
- **Simulated heating and cooling:** The displayed temperature increases when heating is commanded and cools toward the simulated ambient temperature when heating is off.
- **Temperature gauge:** A meter shows the simulated current oven temperature.
- **Power control:** An HMI rocker switch controls the simulated oven's power command.
- **Status indicators:** LEDs show power, temperature ramp-up, target temperature reached, door lock, and safe-to-open conditions.
- **Process sequencing:** A state-based process controller manages oven operation, including ramp-up, at-temperature operation, a dwell timer, and cooling.
- **Alarm monitoring:** The HMI includes an alarm table and an alarm acknowledgment control.
- **High-temperature protection:** An alarm is triggered if the simulated temperature exceeds the configured O-ring temperature limit.
- **Automatic safety trip:** If the temperature rises more than **10°F above the O-ring limit**, the safety logic trips and turns off the simulated oven power command.

## Project Structure

| CODESYS component | Purpose |
| --- | --- |
| `PLC_PRG` | Main program that invokes the function blocks. |
| `GVL_Oven` | Global variables for operator inputs, simulated temperature, indicators, and safety states. |
| `FB_ProcessControl` | Manages operating states, heating commands, and process timing. |
| `FB_SafetyLogic` | Handles overtemperature alarms, shutdown trips, and related safety logic. |
| `FB_TemperatureSimulation` | Simulates heating and cooling based on the heating command. |
| `Visu_Oven` | Operator HMI with controls, gauge, indicators, and alarm table. |
| Alarm Configuration | Configures the alarm system used by the visualization. |

The project also contains task configuration and visualization management objects.

## HMI Overview

The visualization provides:

1. A **rocker switch** and power-status indicator.
2. A **temperature setpoint spinner/input**.
3. A **gauge** displaying the current simulated temperature.
4. **LED indicators** for ramp-up, at-temperature, locked-door, and safe-to-open status.
5. An **alarm table** and **alarm acknowledgment** control.

## Temperature and Safety Logic

The documented simulation uses the following example values:

| Parameter | Documented value |
| --- | --- |
| Simulated ambient temperature | 75°F |
| O-ring temperature limit | 150°F |
| High-temperature alarm condition | Temperature above 150°F |
| Critical shutdown condition | Temperature above 160°F (10°F beyond the limit) |

The values above describe the documented example configuration, not universal safe temperatures for real O-rings. Actual O-ring limits depend on material specifications.

**Important:** The shutdown in this project switches off the *simulated oven control output*; it does not physically disconnect a heater or stop an industrial PLC. A real industrial oven would require independently engineered and validated safety controls.

## How to Open and Run the Simulation

1. Download the `Industrial_oven.project` file from this repository.
2. Open it using **CODESYS V3.5 SP21 Patch 3**.
3. Allow CODESYS to resolve any required device or library dependencies, if prompted.
4. Select **Build → Build** and check for build errors.
5. Use **Online → Simulation** for CODESYS simulation mode, or connect to an appropriately installed and configured **CODESYS Control Win V3 x64** runtime.
6. Select **Online → Login**, then start the application.
7. Open **`Visu_Oven`** to view and operate the simulated HMI.
8. Set the target temperature, turn the oven on, and observe the gauge, status indicators, and alarms.

Menu wording and runtime setup may vary slightly depending on installed CODESYS components. You do **not** need to connect a physical PLC.

## Suggested Verification Scenarios

| Scenario | Expected simulation behavior |
| --- | --- |
| Power switched on with a valid setpoint | Simulated temperature ramps toward the target; ramp-up indicator activates. |
| Target temperature reached | At-temperature indication activates and the process follows its configured timed sequence. |
| Heating switched off | Simulated oven temperature cools toward ambient. |
| Temperature exceeds O-ring limit | High-temperature alarm becomes active. |
| Temperature exceeds the limit by more than 10°F | Safety trip disables the simulated oven power command. |
| Oven has cooled sufficiently | Safe-to-open status is indicated according to the configured logic. |
| Alarm is acknowledged | The configured acknowledgment logic responds, subject to the underlying alarm condition. |

The project documentation includes screenshots of the HMI, PLC logic, flowchart, and application testing.

## Limitations

- The oven, heater, temperature measurement, and door status are **simulated**, not connected to physical equipment.
- Temperature changes are generated by software logic and do not represent a calibrated thermal model.
- This project is intended for **education and demonstration**, not for direct industrial deployment.

## Academic Context

Developed as a final project for **BCA153 — Computer Applications in the Industry**, Department of Computer Applications, College of Computer Studies, **Mindanao State University – Iligan Institute of Technology (MSU-IIT)**.

**Project members:** Binyusoph P. Sansarona and KJ C. Villanueva.

---

*Industrial Oven Control System — PLC programming and HMI simulation using CODESYS.*
