
# Full-Order Flux Observer with MRAS for Induction Motor Drives

## Author
Hao WU

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