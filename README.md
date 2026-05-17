# Lateral Vehicle Guidance System using MATLAB/Simulink

## Overview

This project presents the modeling, simulation and validation of a lateral vehicle guidance system developed using a Model Based Design (MBD) approach under MATLAB/Simulink.

The objective is to design a control architecture capable of ensuring trajectory tracking on a winding road while minimizing the lateral tracking error and maintaining vehicle stability.

The developed system integrates:

- a 2D kinematic vehicle model,
- trajectory generation,
- a PID-based lateral controller,
- Stateflow supervision,
- MIL, SIL and PIL validation workflows,
- 2D and 3D visualization tools.

This project was developed as part of the Model Based Design module.

---

# Project Objectives

The main objective of the project is to design and validate a lateral guidance system able to follow a reference trajectory under different operating conditions.

The project focuses on:

- modeling the vehicle dynamics,
- implementing a closed-loop control system,
- minimizing trajectory tracking errors,
- validating generated embedded code,
- analyzing system behavior through simulations and visualization tools.

---

# System Description

The implemented architecture is based on a closed-loop control structure composed of several interconnected subsystems:

- Environment subsystem responsible for trajectory generation,
- Vehicle dynamic model (Plant),
- PID controller,
- Stateflow supervision logic,
- Visualization and monitoring blocks.

The controller continuously computes the steering command according to the trajectory tracking error and vehicle orientation error.

---

# Vehicle Dynamic Model

The vehicle is modeled using a simplified 2D kinematic bicycle model.

The system equations are defined as:

\[
\dot{x} = v \cos(\psi)
\]

\[
\dot{y} = v \sin(\psi)
\]

\[
\dot{\psi} = \frac{v}{L} \tan(\delta)
\]

Where:

| Variable | Description |
|---|---|
| \(x\) | Longitudinal position |
| \(y\) | Lateral position |
| \(\psi\) | Vehicle orientation angle |
| \(\delta\) | Steering angle |
| \(v\) | Vehicle speed |
| \(L\) | Vehicle wheelbase |

The adopted assumptions are:

- constant longitudinal speed,
- planar vehicle motion,
- simplified kinematic behavior,
- direct steering actuation.

---

# Simulink Architecture

The global Simulink architecture is organized into multiple subsystems in order to ensure modularity and readability.

## Global Architecture

_Insert global Simulink architecture image here._

The main subsystems are:

### Environment

Responsible for:

- generating reference trajectories,
- selecting simulation scenarios,
- introducing disturbances.

### Controller

Responsible for:

- lateral error computation,
- orientation error computation,
- steering command generation using PID control.

### Plant

Implements the vehicle dynamic model.

### Supervision

Implements the Stateflow finite state machine managing operating modes.

### Visualization

Contains:

- XY Graph visualization,
- scopes,
- vehicle visualization,
- 3D simulation.

---

# Reference Trajectory Generation

Several reference trajectories are implemented to evaluate system behavior under different conditions.

The scenario selection is performed dynamically using a Dashboard interface integrated into Simulink.

## Scenario Generation Block

_Insert scenario generation block image here._

Implemented scenarios include:

- nominal sinusoidal trajectory,
- fast varying trajectory,
- perturbation scenario,
- high curvature trajectory.

---

# PID Controller Design

The lateral guidance system uses a PID controller to minimize tracking errors.

The controller relies on:

- lateral trajectory error,
- orientation error.

The PID controller is implemented directly under Simulink using PID Controller blocks.

## PID Controller Implementation

_Insert PID controller image here._

The controller parameters are tuned using the Simulink PID Tuner tool in order to obtain a compromise between:

- tracking precision,
- system stability,
- response speed.

## PID Tuning

_Insert PID tuner image here._

---

# Stateflow Supervision

The system operating modes are managed using Stateflow.

The finite state machine includes the following states:

- Init,
- Standby,
- Nominal,
- Emergency.

Transitions depend on:

- system activation,
- fault detection,
- trajectory error thresholds.

## Stateflow FSM

_Insert Stateflow diagram image here._

---

# MIL Validation

The first validation phase is performed using a Model-In-the-Loop (MIL) approach.

The complete control architecture is simulated directly in Simulink in order to evaluate system behavior under multiple operating conditions.

## MIL Simulation

_Insert MIL simulation image here._

The obtained results show:

- good trajectory tracking,
- stable vehicle behavior,
- low tracking error under nominal conditions.

---

# SIL Validation

Software-In-the-Loop validation is used to verify the consistency between:

- the Simulink model,
- the generated embedded code.

The controller code is automatically generated and executed in a software environment.

## SIL Architecture

_Insert SIL validation image here._

The comparison between MIL and SIL outputs confirms that the generated code reproduces the same behavior as the original Simulink model.

---

# PIL Validation

Processor-In-the-Loop validation allows execution of the generated code directly on an embedded target.

In this project, the controller is deployed on an Arduino board while maintaining the simulation environment under Simulink.

## PIL Validation

_Insert PIL validation image here._

The obtained results validate:

- correct embedded execution,
- consistency between processor execution and simulation model.

---

# 2D and 3D Visualization

Visualization tools are integrated to facilitate system analysis and result interpretation.

The project includes:

- 2D trajectory visualization,
- scope monitoring,
- real-time vehicle visualization,
- 3D simulation environment.

## 2D Visualization

_Insert 2D trajectory image here._

## 3D Simulation

_Insert 3D simulation image here._

The 3D simulation provides a realistic representation of vehicle motion and trajectory tracking behavior.

---

# Technologies and Tools

The project was developed using:

- MATLAB
- Simulink
- Stateflow
- Simulink Dashboard
- Simulink PID Tuner
- Simulink 3D Animation
- Embedded Coder
- Arduino

---

# Validation Workflow

The project follows a progressive Model Based Design validation methodology:

1. System modeling
2. Simulation under MATLAB/Simulink
3. MIL validation
4. SIL validation
5. PIL validation
6. Visualization and analysis

---

# Academic Context

Module: Model Based Design (MBD)

Field: Embedded Systems and Artificial Intelligence

Academic Year: 2024/2025

---

# Author

Yasmine Sbai

---

# Supervisor

M. Anass Mansouri
