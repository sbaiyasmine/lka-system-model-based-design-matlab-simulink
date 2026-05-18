# Lane Keeping Assist (LKA) System under MATLAB/Simulink

## Project Overview

This project presents the design, modeling and validation of a Lane Keeping Assist (LKA) system developed under MATLAB/Simulink using a Model-Based Design (MBD) approach.

The objective of the system is to ensure autonomous lateral vehicle guidance on a complex sinuous road while minimizing the trajectory tracking error using a PID controller associated with Stateflow supervision.

The developed system integrates:

- a simplified 2D vehicle dynamic model,
- a trajectory generation environment,
- a PID steering controller,
- Stateflow supervision,
- MIL / SIL / PIL validations,
- 2D and 3D visualization.

---

# SysML Modeling

A SysML modeling phase was carried out in order to structure the system architecture and define the interactions between the different subsystems.

The SysML analysis includes:

- requirements diagrams,
- use case diagrams,
- block definition diagrams,
- internal block diagrams,
- functional architecture diagrams.

This modeling phase allows a clear transition between system requirements and Simulink implementation.

---

# Simulink Global Architecture

The global Simulink model is organized around several clearly separated subsystems:

- Environment
- Error Computation
- PID Controller
- Plant
- Sensors
- Stateflow Supervision
- Visualization

The adopted architecture follows a modular Model-Based Design methodology.

<p align="center">
  <img src="images/archi_simulink.png" width="950">
</p>

<p align="center">
Global Simulink architecture of the Lane Keeping Assist system.
</p>

---

# Environment and Trajectory Generation

The Environment subsystem generates the reference trajectory used by the controller.

The reference road is modeled using a combination of sinusoidal functions in order to generate a complex sinuous road.

The Environment subsystem generates:

- reference lateral position,
- reference orientation,
- disturbances,
- test scenarios.

<p align="center">
  <img src="images/environment.png" width="850">
</p>

<p align="center">
Environment subsystem and trajectory generation model.
</p>

---

# Vehicle Dynamic Model

The vehicle is modeled using a simplified 2D kinematic bicycle model.

The adopted model represents:

- longitudinal motion,
- lateral motion,
- vehicle orientation.

The system equations are:

<p align="center">

dx/dt = v cos(ψ)

dy/dt = v sin(ψ) + dy_pert

dψ/dt = (v / L) tan(δ)

</p>

Where:

| Variable | Description |
|---|---|
| x | Longitudinal position |
| y | Lateral position |
| ψ | Vehicle orientation |
| δ | Steering angle |
| v | Vehicle speed |
| L | Vehicle wheelbase |
| dy_pert | Lateral disturbance |

---

# Simplifying Assumptions

The adopted model is based on the following assumptions:

- constant longitudinal speed,
- planar 2D motion,
- moderate steering angles,
- no complex tire dynamics,
- no load transfer effects,
- simplified bicycle vehicle representation.

These assumptions allow a simple and stable model compatible with a pedagogical MBD approach.

---

# PID Controller

The lateral guidance system is controlled using a PID controller.

The controller continuously computes the steering angle required to minimize the trajectory tracking error.

The controller acts on:

- lateral position error,
- orientation error.

<p align="center">
  <img src="images/controller.png" width="750">
</p>

<p align="center">
PID controller implementation under Simulink.
</p>

---

# Stateflow Supervision

System supervision is implemented using a Stateflow finite state machine.

The Stateflow logic manages:

- system initialization,
- operational activation,
- fault management,
- emergency behavior.

The implemented states are:

- Init
- Standby
- Nominal
- Emergency

---

# MIL / SIL / PIL Validation

The project integrates several validation levels according to the Model-Based Design methodology.

## MIL — Model In The Loop

MIL validation is used to validate the complete Simulink model behavior.

This phase verifies:

- vehicle dynamics,
- trajectory tracking,
- controller performance.

---

## SIL — Software In The Loop

SIL validation compares:

- Simulink model behavior,
- generated controller code behavior.

This step validates automatic code generation consistency.

---

## PIL — Processor In The Loop

PIL validation evaluates the controller compiled on a processor target.

This phase allows:

- execution time analysis,
- embedded controller validation,
- real-time compatibility verification.

---

# 2D Visualization

A 2D visualization is used to analyze:

- reference trajectory,
- real vehicle trajectory,
- lateral tracking error evolution.

<p align="center">
  <img src="images/scen2_2D.png" width="850">
</p>

<p align="center">
2D trajectory tracking visualization.
</p>

---

# 3D Simulation

A 3D scene is integrated in order to visualize the vehicle moving on a complex sinuous road.

The 3D simulation provides:

- realistic vehicle visualization,
- dynamic behavior interpretation,
- complete project demonstration.

<p align="center">
  <img src="images/3D_simulation.png" width="950">
</p>

<p align="center">
3D vehicle visualization under Simulink.
</p>

---

# Obtained Results

The obtained simulation results show:

- correct trajectory tracking,
- significant lateral error reduction,
- stable vehicle behavior,
- coherent response under different scenarios.

The implemented test scenarios include:

- nominal scenario,
- trajectory change,
- lateral disturbance,
- simplified fault scenario.

---

# Software and Tools

The project was developed using:

- MATLAB
- Simulink
- Stateflow
- Simulink 3D Animation
- SysML

---

# Future Improvements

Possible future improvements include:

- variable speed integration,
- more realistic dynamic vehicle model,
- tire force modeling,
- Hardware-In-the-Loop (HIL) validation,
- real sensor integration,
- advanced 3D road environment generation.

---
