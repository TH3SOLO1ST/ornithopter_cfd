# Ornithopter CFD Simulation

## Overview

This repository contains a 2D incompressible Navier-Stokes solver implemented in Python to simulate the fluid dynamics around an ornithopter wing. The code models flapping and pitching motion using a dynamic mesh with Radial Basis Function (RBF) interpolation, computes lift and thrust forces, and visualizes the results.

The simulation uses the Chorin projection method to solve the Navier-Stokes equations, optimized with JAX for performance. It includes:
- Dynamic mesh deformation based on wing kinematics.
- Computation of lift and thrust forces.
- Visualization of lift, thrust, and velocity field with deformed mesh.
- Data saving in `.npz` format for further analysis.

The project is designed to run in Google Colab, making it accessible without local setup.

## Features

- **Dynamic Mesh**: Uses RBF interpolation to deform the mesh according to wing motion.
- **Force Calculation**: Computes lift and thrust based on pressure and velocity fields.
- **Visualization**: Generates plots for lift, thrust, and velocity field with deformed mesh.
- **Optimization**: Leverages JAX for efficient advection computation.
- **3D Placeholder**: Includes a basic 3D mesh generation option (requires Gmsh).

## Requirements

- `numpy>=1.20`
- `scipy>=1.7`
- `matplotlib>=3.4`
- `jax>=0.4`
- `jaxlib>=0.4`
- (Optional) `gmsh` for 3D mesh generation

## Installation

### Google Colab Setup

1. Open a new notebook at [Google Colab](https://colab.research.google.com).
2. Install dependencies:
   ```bash
   (Optional for 3D mesh: !pip install gmsh)
3. Upload the config.json file to the Colab environment:

Click the folder icon in the left sidebar.
Click "Upload" and select config.json.
Alternatively, create it in Colab:

%%writefile config.json
{
    "nx": 50,
    "ny": 50,
    "t_max": 0.5,
    "c": 1.0,
    "f": 7.0,
    "h": 0.05,
    "alpha_max_deg": 10,
    "U_inf": 10.0,
    "rho": 1.225,
    "nu": 0.01,
    "dt": 0.0005
}

4. Upload and run the ornithopter_cfd.py script:

   %%writefile ornithopter_cfd.py
# Paste the contents of ornithopter_cfd.py here
!python ornithopter_cfd.py

5. Download outputs:

   from google.colab import files
files.download("ornithopter_results.png")
files.download("ornithopter_data.npz")

(Optional) Save to Google Drive:

!cp ornithopter_results.png /content/drive/MyDrive/
!cp ornithopter_data.npz /content/drive/MyDrive/

##Local Setup
1. Clone the repository:

git clone https://github.com/your-username/ornithopter-cfd.git
cd ornithopter-cfd

2. Install dependencies:

pip install numpy scipy matplotlib jax jaxlib
(Optional for 3D mesh: pip install gmsh)

3. Run the script:

python ornithopter_cfd.py


##Usage

  Edit config.json to adjust simulation parameters (e.g., grid size, flapping frequency, viscosity).
  Run the script to generate ornithopter_results.png (plots) and ornithopter_data.npz (data).
  Analyze the plots for lift, thrust, and velocity field behavior.

##Configuration
The config.json file contains the following parameters:

  nx, ny: Grid dimensions.
  t_max: Total simulation time (s).
  c: Chord length (m).
  f: Flapping frequency (Hz).
  h: Flapping amplitude (m).
  alpha_max_deg: Maximum pitching angle (degrees).
  U_inf: Freestream velocity (m/s).
  rho: Fluid density (kg/m³).
  nu: Kinematic viscosity (m²/s).
  dt: Time step (s).

##Outputs
  ornithopter_results.png: Three subplots showing:
    Lift vs. time.
    Thrust vs. time.
    Velocity field and deformed mesh.
  ornithopter_data.npz: Saved arrays for lift, thrust, velocity (u, v), and mesh coordinates (X, Y).

##Troubleshooting
  Mesh Coordinates Out of Bounds: Reduce h or alpha_max_deg in config.json if warnings appear.
  Empty Plots: Check console output for warnings (e.g., "Velocity field is invalid") and share logs if needed.
  Dependency Issues: Re-run the installation commands.

##Contributing
Feel free to fork this repository, submit issues, or propose enhancements (e.g., vorticity plots, 3D solver). Pull requests are welcome!

##License
MIT License.

##Acknowledgements
Built with assistance from Grok 3, created by xAI.
Inspired by ornithopter fluid dynamics research.

##Contact
For questions or support, please open an issue or contact excel3227@gmail.com


