
# 1. Full-Order Flux Observer with MRAS for Induction Motor Drives

> Simulink implementation of a full-order flux observer (FOO) combined with Model Reference Adaptive System (MRAS) for sensorless induction motor control.

## Features
- Full-order state observer with current error feedback for accurate stator/rotor flux estimation
- MRAS-based rotor speed estimation for encoderless operation, with PI adaptation law
- Single-parameter pole placement design, balancing convergence speed and noise immunity
- Low-speed error signal switching strategy for improved stability near zero speed
- Complete stability derivation based on Lyapunov theory and Popov hyperstability criterion

## Architecture
The system consists of two tightly coupled closed-loop modules:
1.  **Full-Order Flux Observer**: Uses measured stator voltages and currents to estimate αβ-axis flux linkages, with current error feedback to correct estimation drift.
2.  **MRAS Speed Adaptation**: Compares outputs from the reference voltage model and the adjustable observer model, then updates the speed estimate via PI regulation.

## Getting Started
### Prerequisites
- MATLAB / Simulink
- Basic knowledge of induction motor vector control

### Run Simulation
1.  Open the Simulink model file.
2.  Set motor parameters in the workspace.
3.  Tune the observer pole coefficient `K` (typical range: 3–6) to match your bandwidth requirement.
4.  Run the simulation and verify flux / speed estimation waveforms.

## Parameter Tuning Reference
| Parameter | Design Rule |
|-----------|-------------|
| Observer bandwidth | 3–6 × motor electrical bandwidth (recommended) |
| Stator flux gain `k₁` | `Rₛ · (K² − 1)` |
| Rotor flux gain `k₃` | Derived from pole scaling condition |
| MRAS PI gains | Match observer bandwidth; `Kᵢ ≈ Kₚ / (5·Tᵣ)` |

## License
For research and educational use only.

---

## 2. Brief Outline of the paper (FullOrderObserverDesignWithMRAS.docx)

1.  **Introduction & Core Architecture**
    -   Objective: Sensorless flux and speed estimation for induction motor drives
    -   Solution: Full-order flux observer (FOO) + Model Reference Adaptive System (MRAS)
    -   Scope exclusion: Parameter tuning, fault diagnosis, multi-observer cooperation, control strategy design

2.  **Theoretical Foundations**
    -   Induction motor model in stationary αβ reference frame
    -   Luenberger full-order state observer principle
    -   Lyapunov stability theory for error convergence
    -   Discrete numerical implementation (Forward Euler method)

3.  **Full-Order Observer (FOO) Core Design**
    -   4-dimensional state-space representation
    -   Current error feedback structure and gain matrix
    -   Single-parameter pole placement methodology (K coefficient)
    -   Bandwidth trade-off strategy for different operating conditions

4.  **MRAS Speed Estimation Integration**
    -   Reference model (voltage model) vs. adjustable model (current model)
    -   Error signal construction (flux cross-product; low-speed switching to current error)
    -   PI-type adaptation law design
    -   Closed-loop coupling mechanism between FOO and MRAS

5.  **Stability Analysis**
    -   Asymptotic stability of the observer error subsystem
    -   Popov hyperstability criterion for the MRAS loop
    -   Sufficient stability conditions for the combined system
    -   Conditional convergence conclusion

6.  **Parameter Design Example**
    -   Analytical formulas for observer gains (k₁, k₃, k₄)
    -   Empirical tuning rule for observer bandwidth ratio
    -   MRAS PI gain calculation guidelines
    -   Numerical verification with real motor parameters

7.  **Test & Validation**
    -   Simulation results: Speed tracking performance
    -   Test bench findings: Low-speed instability during deceleration (under investigation)

8.  **Summary**
    -   Key advantages: Robustness, balanced dynamic performance, real-time feasibility
    -   Application scenarios: Sensorless operation, online parameter self-calibration

---
