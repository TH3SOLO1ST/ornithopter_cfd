# Ornithopter CFD Simulation

---

## Overview

This repository features a 2D incompressible Navier-Stokes solver, implemented in Python, designed to simulate fluid dynamics around an ornithopter wing. The solver models **flapping and pitching motion** using a dynamic mesh with **Radial Basis Function (RBF) interpolation**, computes **lift and thrust forces**, and provides visualizations of the results.

The simulation utilizes the Chorin projection method to solve the Navier-Stokes equations, optimized for performance with **JAX**. Key functionalities include:

* **Dynamic mesh deformation** based on predefined wing kinematics.
* **Computation of lift and thrust forces**.
* **Visualization** of lift, thrust, and the velocity field superimposed on the deformed mesh.
* **Data saving** in `.npz` format for subsequent analysis.

This project is configured to run seamlessly in **Google Colab**, making it highly accessible without requiring complex local setups.

---

## Features

* **Dynamic Mesh**: Employs RBF interpolation to deform the computational mesh in response to wing motion.
* **Force Calculation**: Accurately computes lift and thrust based on the simulated pressure and velocity fields.
* **Visualization**: Generates informative plots for lift, thrust, and the velocity field, showcasing the deformed mesh.
* **Optimization**: Leverages the JAX library for efficient advection computation, enhancing performance.
* **3D Placeholder**: Includes a foundational option for 3D mesh generation (requires `Gmsh`).

---

## Requirements

The following Python libraries are required:

* `numpy>=1.20`
* `scipy>=1.7`
* `matplotlib>=3.4`
* `jax>=0.4`
* `jaxlib>=0.4`
* (Optional) `gmsh` for 3D mesh generation

---

## Installation

### Google Colab Setup

For the most straightforward experience, we recommend using Google Colab:

1.  Open a new notebook at [Google Colab](https://colab.research.google.com).
2.  **Install dependencies**:
    ```bash
    !pip install numpy scipy matplotlib jax jaxlib
    # (Optional for 3D mesh: !pip install gmsh)
    ```
3.  **Upload `config.json`**:
    * Click the **folder icon** in the left sidebar.
    * Click "**Upload**" and select your `config.json` file.
    * Alternatively, you can create it directly in Colab:
        ```python
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
        ```
4.  **Upload and run `ornithopter_cfd.py`**:
    * Similar to `config.json`, upload your `ornithopter_cfd.py` script.
    * Then, run it from a Colab cell:
        ```python
        %%writefile ornithopter_cfd.py
        # [Paste the content of your ornithopter_cfd.py script here]

        !python ornithopter_cfd.py
        ```
5.  **Download outputs**:
    ```python
    from google.colab import files
    files.download("ornithopter_results.png")
    files.download("ornithopter_data.npz")
    ```
    (Optional) **Save to Google Drive**:
    ```bash
    !cp ornithopter_results.png /content/drive/MyDrive/
    !cp ornithopter_data.npz /content/drive/MyDrive/
    ```

### Local Setup

If you prefer to run the simulation locally:

1.  **Clone the repository**:
    ```bash
    git clone [https://github.com/your-username/ornithopter-cfd.git](https://github.com/your-username/ornithopter-cfd.git)
    cd ornithopter-cfd
    ```
2.  **Install dependencies**:
    ```bash
    pip install numpy scipy matplotlib jax jaxlib
    # (Optional for 3D mesh: pip install gmsh)
    ```
3.  **Run the script**:
    ```bash
    python ornithopter_cfd.py
    ```

---

## Usage

* **Edit `config.json`** to adjust simulation parameters such as grid size, flapping frequency, or fluid viscosity.
* **Run the script** to generate `ornithopter_results.png` (containing plots) and `ornithopter_data.npz` (containing raw simulation data).
* **Analyze the generated plots** to observe lift, thrust, and the behavior of the velocity field.

---

## Configuration

The `config.json` file allows you to customize the simulation with the following parameters:

* `nx`, `ny`: Grid dimensions.
* `t_max`: Total simulation time in seconds ($s$).
* `c`: Chord length in meters ($m$).
* `f`: Flapping frequency in Hertz ($Hz$).
* `h`: Flapping amplitude in meters ($m$).
* `alpha_max_deg`: Maximum pitching angle in degrees ($^\circ$).
* `U_inf`: Freestream velocity in meters per second ($m/s$).
* `rho`: Fluid density in kilograms per cubic meter ($kg/m^3$).
* `nu`: Kinematic viscosity in square meters per second ($m^2/s$).
* `dt`: Time step in seconds ($s$).

---

## Outputs

Upon successful execution, the simulation generates two main output files:

* **`ornithopter_results.png`**: This image file contains three subplots:
    * Lift versus time.
    * Thrust versus time.
    * Velocity field visualized with the deformed mesh.
* **`ornithopter_data.npz`**: This compressed NumPy archive stores arrays for further analysis, including:
    * Lift forces.
    * Thrust forces.
    * Velocity components ($u$, $v$).
    * Mesh coordinates ($X$, $Y$).

---

## Troubleshooting

* **Mesh Coordinates Out of Bounds**: If you encounter warnings related to mesh coordinates, try reducing the `h` (flapping amplitude) or `alpha_max_deg` (maximum pitching angle) values in `config.json`.
* **Empty Plots**: Check the console output for any warnings (e.g., "Velocity field is invalid"). If issues persist, please share the logs when seeking assistance.
* **Dependency Issues**: If you face problems with required libraries, re-run the installation commands specific to your setup (Google Colab or Local).

---

## Contributing

Contributions are welcome! Feel free to fork this repository, submit issues, or propose enhancements such as vorticity plots or a full 3D solver. Pull requests are highly appreciated.

---

## License

This project is licensed under the [MIT License](LICENSE).

---

## Acknowledgements

* Built with assistance from Grok 3, created by xAI.
* Inspired by ongoing research in ornithopter fluid dynamics.
