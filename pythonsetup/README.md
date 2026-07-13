# 3D Muon Scattering Tomography Simulator

This project implements a complete, highly optimized, and vectorized 3D Muon Scattering Tomography simulation in Python. It models a realistic cosmic-ray tracking detector system, simulates Multiple Coulomb Scattering (MCS) through a steel container housing an unknown object, reconstructs the muon trajectories, calculates the Point of Closest Approach (POCA) to yield a 3D density map, and classifies the hidden material.

## 🚀 Features

- **Object-Oriented Architecture**: Modular design representing `ScintillatorPlane`, `FiberLayer`, `MAPMT`, `DetectorStack`, `Container`, `HiddenObject`, `Muon`, `Track`, `ScatteringSimulator`, `TrackReconstructor`, `POCAReconstructor`, `MaterialClassifier`, and `Simulation`.
- **Vectorized MCS & Tracking**: Uses NumPy vectorization for intersection, scattering, and least-squares tracking, capable of simulating 100,000 muons in less than a second.
- **Realistic Readout Routing**: Models 100 X-fibers and 100 Y-fibers per plane, including the smooth curved routing around detector edges to the two MAPMT readout modules.
- **3D POCA Reconstruction**: Computes the Point of Closest Approach for scattered tracks and voxelizes the container space into a 1 cm³ grid weighted by the scattering angle squared.
- **Self-Calibrating Classifier**: Compares reconstructed statistics against expected Highland models calibrated to the exact momenta and path lengths of intersecting muons.
- **Interactive 3D Event Display**: Renders detector planes, fiber meshes, MAPMTs, tracks, hit pixels, POCA points, and a voxel density cloud in Plotly.

## 📦 Project Structure

```text
MuonTomography/
├── __init__.py           # Marks directory as package
├── config.py             # Global detector and simulation parameters
├── materials.py          # Material reference database (Air to Uranium)
├── geometry.py           # Vectorized 3D geometry intersection routines
├── fiber.py              # Models optical fibers and 3D bending curves
├── mapmt.py              # Multi-Anode PMT readout representation
├── detector.py           # Represents tracker planes and stack
├── container.py          # Models the steel container and target shapes
├── muon_generator.py     # Simulates cosmic muon fluxes
├── scattering.py         # Propagates particles with Multiple Coulomb Scattering
├── tracking.py           # Fits track segments using least-squares regression
├── reconstruction.py     # Performs POCA voxel mapping and classification
├── visualization.py      # Generates interactive 3D event displays in Plotly
└── main.py               # Orchestrator and CLI interface
```

## 🛠️ Requirements

The project requires Python 3 and the following dependencies:

```bash
pip install numpy plotly
```

## 🏃 How to Run

To run the simulation and performance validation, execute:

```bash
python3 main.py --muons 100000 --runs 5 --val-muons 25000
```

### Options:
- `--muons`: Number of muons to simulate for the detailed single-run (default: `100000`).
- `--runs`: Number of performance validation test iterations (default: `5`).
- `--val-muons`: Number of muons simulated per validation run (default: `25000`).

## 📊 Outputs

Upon execution, the simulator will:
1. Print a detailed summary of the main run (Tungsten Cylinder target).
2. Display ASCII histograms of scattering angle and centroid displacement in the terminal.
3. Save an interactive 3D event display to `muon_tomography_display.html` (viewable in any browser).
4. Run validation loops to report the overall classification accuracy.
