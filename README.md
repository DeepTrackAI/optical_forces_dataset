# Optical Forces Dataset (optical_forces_dataset)

## Overview

This DeepTrackAI repository contains simulated optical force data for a microsphere trapped in an optical tweezer, following the work of [Bronte Ciriza et al., ACS Photonics, 2022](https://doi.org/10.1021/acsphotonics.2c01565). The simulations were generated using the Optical Tweezers in Geometrical Optics (OTGO) toolbox by [Callegari et al., *JOSA B*, 2015](https://doi.org/10.1364/JOSAB.32.000B11).

### Summary
The dataset contains:
- **Theoretical** optical forces along the z-axis (exact analytical solution).
- **Geometrical optics (GO) approximation** results with 100 rays.

### Experimental parameters
- Laser power (**P**): 5 mW  
- Medium refractive index (**nₘ**): 1.33 (water)  
- Particle refractive index (**nₚ**): 1.50 (glass)  
- Particle radius (**R**): 1 μm  
- Focal length (**f**): 0.1 mm  
- Numerical aperture (**NA**): 1.3  
- Beam waist (**w₀**): 0.1 mm  

---

## Dataset Structure

- **`fz_vs_z_theory.txt`**  
  Two columns:  
  1. z-position (μm)  
  2. Theoretical z-component of the optical force Fz (pN)  
  These values serve as the **ground truth** for comparison with GO results and ML predictions.

- **`xyz_go_100rays.npy`**  
  NumPy array (4D) containing the particle positions (x, y, z) where optical forces were calculated.

- **`fxyz_go_100rays.npy`**  
  NumPy array (4D) containing the corresponding force components (Fx, Fy, Fz) at each position in piconewtons.

- **`sphere_100rays/`**  
  Contains approximately **10⁵** optical force data points simulated via OTGO.  
  - Data is split into 101 files: `force_grid_3D=1.txt`, `force_grid_3D=2.txt`, …  
  - Each file contains rows of eight numbers:  
    ```
    R  np  x  y  z  fx  fy  fz
    ```
    where:  
    - **R**: particle radius in meters  
    - **np**: particle refractive index  
    - **x, y, z**: particle position in meters  
    - **fx, fy, fz**: optical force components in newtons  

---

## Original Source

- **Title:** Faster and More Accurate Geometrical-Optics Optical Force Calculation Using Neural Networks  
- **Authors:** David Bronte Ciriza, et al.  
- **Journal:** ACS Photonics, 10, 234–241 (2022)  
- **DOI:** [10.1021/acsphotonics.2c01565](https://doi.org/10.1021/acsphotonics.2c01565)

- **Toolbox:** Computational Toolbox for Optical Tweezers in Geometrical Optics (OTGO)  
- **Authors:** Agnese Callegari, et al.  
- **Journal:** Journal of the Optical Society of America B, 32, B11–B19 (2015)  
- **DOI:** [10.1364/JOSAB.32.000B11](https://doi.org/10.1364/JOSAB.32.000B11)

If you use this dataset in your research, please follow the licensing requirements and properly attribute the original authors.

---

## Dataset Structure

```bash
/optical_forces_dataset  
├── fz_vs_z_theory.txt        # Theoretical Fz vs. z-position (z [μm], Fz [pN])
├── xyz_go_100rays.npy        # (4D array) Particle positions [x, y, z]
├── fxyz_go_100rays.npy       # (4D array) Force components [Fx, Fy, Fz] in pN
└── sphere_100rays/           # ~10^5 GO data points for NN training
    ├── force_grid_3D=1.txt
    ├── force_grid_3D=2.txt
    └── ...
```

---

## How to Access the Data

### Clone the Repository
```bash
git clone https://github.com/DeepTrackAI/optical_forces_dataset.git
cd optical_forces_dataset
```

---

## Usage Example

```python
import numpy as np

# Load theoretical Fz data
z_theory, fz_theory = np.loadtxt("fz_vs_z_theory.txt", unpack=True)

# Load GO simulation data
xyz_go = np.load("xyz_go_100rays.npy")     # positions
fxyz_go = np.load("fxyz_go_100rays.npy")   # forces

# Example: read one of the sphere_100rays files
R, np_val, x, y, z, fx, fy, fz = np.loadtxt("sphere_100rays/force_grid_3D=1.txt", unpack=True)

print("Positions shape:", xyz_go.shape)
print("Forces shape:", fxyz_go.shape)
print("First few Fz theoretical values:", fz_theory[:5])
```

---

## Attribution

### Cite the dataset original paper:
Bronte Ciriza D, et al. *Faster and More Accurate Geometrical-Optics Optical Force Calculation Using Neural Networks*. ACS Photonics, 10: 234–241 (2022). [https://doi.org/10.1021/acsphotonics.2c01565](https://doi.org/10.1021/acsphotonics.2c01565)

```bibtex
@article{bronte2022faster,
  title={Faster and More Accurate Geometrical-Optics Optical Force Calculation Using Neural Networks},
  author={Bronte Ciriza, David and others},
  journal={ACS Photonics},
  volume={10},
  pages={234--241},
  year={2022},
  publisher={ACS},
  doi={10.1021/acsphotonics.2c01565}
}
```

### Cite the toolbox original paper:
Callegari A, et al. *Computational Toolbox for Optical Tweezers in Geometrical Optics*. Journal of the Optical Society of America B, 32: B11–B19 (2015). [https://doi.org/10.1364/JOSAB.32.000B11](https://doi.org/10.1364/JOSAB.32.000B11)

```bibtex
@article{callegari2015comp,
  title={Computational Toolbox for Optical Tweezers in Geometrical Optics},
  author={Callegari, Agnese and others},
  journal={JOSA B},
  volume={32},
  pages={B11--B19},
  year={2015},
  publisher={Optica},
  doi={10.1364/JOSAB.32.000B11}
}
```

---

## License

This repository is released under the **MIT License**.  
You are free to use, modify, and distribute this work, provided that you include the original license notice and attribution.
