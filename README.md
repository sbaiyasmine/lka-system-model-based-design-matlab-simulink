# 🚗 LKA System – Model Based Design using MATLAB/Simulink

## 📌 Project Overview

This project presents the design, modeling and validation of a **Lateral Guidance System (LKA – Lane Keeping Assistance)** developed using a **Model Based Design (MBD)** methodology under **MATLAB/Simulink**.

The objective is to control a vehicle moving on a winding road while minimizing the lateral trajectory error using a PID controller and Stateflow supervision.

The project includes:

- Vehicle dynamic modeling
- Trajectory generation
- PID lateral controller
- Stateflow supervision
- MIL / SIL / PIL validation
- 2D and 3D visualization
- SysML system modeling

---

# 🧠 Main Features

✅ 2D kinematic bicycle vehicle model  
✅ Trajectory tracking on sinusoidal roads  
✅ PID lateral controller  
✅ Stateflow finite state machine (FSM)  
✅ Dashboard for scenario selection  
✅ Multiple simulation scenarios  
✅ MIL / SIL / PIL validation workflow  
✅ 2D trajectory visualization  
✅ 3D vehicle simulation  

---

# 🏗️ System Architecture

The global architecture is organized into several subsystems:

- **Environment**
  - Reference trajectory generation
  - Scenario management

- **Controller**
  - Lateral and orientation error computation
  - PID steering control

- **Plant**
  - Vehicle dynamic model

- **Supervision**
  - Stateflow FSM

- **Visualization**
  - 2D plots
  - Scopes
  - 3D simulation

---

# 📂 Repository Structure

```text
.
├── README.md
├── simulink
│   ├── MIL
│   │   ├── MIL.slx
│   │   ├── MIL_Visualisation.slx
│   │   └── visualisation.slx
│   │
│   ├── SIL
│   │   ├── SIL_controller.slx
│   │   ├── SIL_MIL.slx
│   │   ├── controller_pbs.mexw64
│   │   └── controller_sbs.mexw64
│   │
│   └── PIL
│       ├── PIL_controller.slx
│       └── PIL_MIL.slx
│
├── docs
│   └── report.pdf
│
└── images
    ├── architecture.png
    ├── stateflow.png
    ├── simulation2D.png
    └── simulation3D.png
```

---

# ⚙️ Vehicle Dynamic Model

The vehicle is modeled using a simplified 2D kinematic bicycle model.

## Model Equations

\[
\dot{x} = v \cos(\psi)
\]

\[
\dot{y} = v \sin(\psi)
\]

\[
\dot{\psi} = \frac{v}{L}\tan(\delta)
\]

Where:

- \(x\): longitudinal position
- \(y\): lateral position
- \(\psi\): yaw angle
- \(\delta\): steering angle
- \(v\): vehicle speed
- \(L\): wheelbase

---

# 🎯 Control Strategy

The steering command is generated using a PID controller based on:

- lateral error
- orientation error

The PID parameters are tuned using:

- **Simulink PID Tuner**

---

# 🔄 Stateflow Supervision

The FSM manages system operating modes:

- Init
- Standby
- Nominal
- Emergency

Transitions depend on:

- system activation
- trajectory error
- fault detection

---

# 🧪 Validation Workflow

## ✅ MIL – Model In the Loop

Validation of the control algorithm directly in Simulink.

### Tested Scenarios

- Nominal trajectory
- Fast trajectory variations
- Perturbation injection
- High curvature trajectory

---

## ✅ SIL – Software In the Loop

Generated controller code is executed in a software environment and compared with the original model.

### Result

✔️ No difference between MIL and SIL outputs.

---

## ✅ PIL – Processor In the Loop

The generated code is deployed and executed on an Arduino target.

### Objective

- Validate embedded execution
- Verify generated code behavior on real processor

---

# 📊 Visualization

## 2D Visualization

- XY Graph trajectory tracking
- Scope analysis
- Real-time signals

## 3D Simulation

A 3D scene is integrated to visualize:

- vehicle movement
- road tracking
- steering behavior

---

# 🛠️ Tools & Technologies

- MATLAB
- Simulink
- Stateflow
- PID Tuner
- Simulink Dashboard
- Simulink 3D Animation
- Arduino (PIL validation)

---

# 📚 SysML Modeling

The project also includes SysML analysis and modeling:

- Use Case Diagram
- Requirement Diagram
- BDD Diagram
- IBD Diagram
- State Machine Diagram

---

# 🚀 How to Run

## Open MATLAB

Then open:

```matlab
MIL.slx
```

Run the simulation using:

```matlab
Run
```

Use the Dashboard knob to switch between scenarios.

---

# 📈 Project Objectives

- Understand Model Based Design workflow
- Design a lateral guidance system
- Validate embedded control architecture
- Apply MIL/SIL/PIL methodologies
- Integrate supervision and visualization

---

# 👨‍💻 Author

**Yasmine Sbai**  
Embedded Systems & Artificial Intelligence Engineering Student  
INSEA – Morocco

---

# 👨‍🏫 Supervisor

**M. Anass Mansouri**

---

# 📄 Academic Context

Mini Project – Model Based Design (MBD)  
Academic Year: 2024/2025

---

# 📷 Suggested Images to Add

You can create an `images/` folder and add:

| Image | Description |
|---|---|
| architecture.png | Global Simulink architecture |
| stateflow.png | FSM Stateflow |
| simulation2D.png | 2D trajectory tracking |
| simulation3D.png | 3D vehicle simulation |
| sil_validation.png | MIL/SIL comparison |
| pid_tuner.png | PID tuning |

---

# ⭐ Future Improvements

- Advanced dynamic vehicle model
- MPC controller
- Sensor fusion
- Real-time HIL platform
- Autonomous driving extensions
- Obstacle avoidance
