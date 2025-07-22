# Program settings
To configure the settings for a calculation using the __DIALECT__ program, the file __dialect.toml__ has to be created. You can either create the file yourself or you can run the program in a directory without the configuration file:
```sh
/your/path/to/DIALECT/dialect file.xyz
```
The __dialect.toml__ will then be created using the standard values of the program. 
The settings of the file dialect.toml are explained in the following sections.

---

## General Settings

```toml
jobtype = "sp"   # Type of calculation. Options:
                 # - "sp" (single-point energy calculation)
                 # - "opt" (geometry optimization)
                 # - "grad" (gradient evaluation)
                 # - "hessian" (Hessian matrix calculation)
                 # - "dynamics" (molecular dynamics)
                 # - "monomer_identification" (get the monomer index that corresponds to atomic coordinates)
                 # - "initial_conditions" (Wigner sampling for dynamics)
                 # - "polariton" (exciton-polariton simulation)
                 # - "tdm_ehrenfest" (create the TDMs and/or particle and hole densities along a trajectory of Ehrenfest FMO-LC-TDDFTB)

verbose = 0      # Level of printed output:
                 # - -1: minimal output (silent mode)
                 # -  0: normal/default verbosity
                 # -  1: verbose mode (some debug info)
```

---

## Tight-Binding Method Options

```toml
[tight_binding]
use_dftb = true                  # Enable standard DFTB method (density-functional tight-binding)
use_xtb1 = false                 # Use GFN1-xTB method instead of DFTB (as of now, only ground state properties are supported)
use_gaussian_gamma = true        # Use Gaussian functions to model the gamma matrix (Coulomb interaction); set to false for Slater functions (as most DFTB parametrisations employ Slater functions, we recommend to set this option to false for esternal Slater-Koster parameters)
use_shell_resolved_gamma = false # Allow different Hubbard parameters for different orbital types (s, p, d) instead of one uniform value per atom
```

---

## Fragment Molecular Orbital (FMO) Settings

```toml
[fmo]
use_fmo = false           # Enable FMO method for fragment-based calculations
vdw_scaling = 2.0         # Controls fragmentation behavior:
                          # - Higher values lead to looser fragment pairing
                          # - Controls the number of monomer pairs and ES-DIM pairs
```

---

## Molecular System Information

```toml
[mol]
charge = 0                # Total charge of the system
multiplicity = 1          # Spin multiplicity. Currently, only singlet (1) is supported
```

---

## SCF Convergence Criteria

```toml
[scf]
scf_max_cycles = 250           # Max number of iterations in the self-consistent charge (SCC) loop
scf_charge_conv = 0.00001      # Convergence threshold for charge density between SCC steps
scf_energy_conv = 0.00001      # Convergence threshold for energy between SCC steps
```

---

## Long-Range Corrections

```toml
[lc]
long_range_correction = true   # Apply long-range correction (important for accurate CT excitation energies)
long_range_radius = 3.03       # Radius for applying long-range corrections (in au)
```

---

## DFTB3 Parameters

```toml
[dftb3]
use_dftb3 = false               # Enable DFTB3 (third-order corrections)
use_gamma_damping = false       # Use damping for gamma matrix
hubbard_derivatives = [1.0, 1.0] # Values of the derivatives of the Hubbard U w.r.t. charge for each element (ordered by Z)
```

---

## Geometry Optimization Options

```toml
[opt]
state_to_optimize = 0                  # Electronic state to be optimized (0 = ground state)
geom_opt_max_cycles = 500             # Max number of optimization steps
geom_opt_tol_displacement = 300.0     # Tolerance for geometry displacement, 300 * 10^-6 as default
geom_opt_tol_gradient = 1200.0        # Tolerance for gradient norm (controls convergence), 1200 * 10^-6 as default
geom_opt_tol_energy = 1.0             # Energy change threshold for convergence, 1.0 * 10^-6 as default
use_bfgs = true                       # Use LBFGS optimizer
use_line_search = true               # Enable line search for better step size in optimization
```

---

## Excited State Calculations

```toml
[excited]
calculate_excited_states = false       # Enable excited state calculation
nstates = 10                           # Number of excited states to calculate
davidson_iterations = 100              # Max iterations in the Davidson solver
davidson_subspace_multiplier = 10      # Controls the max subspace size: subspace = nstates * multiplier
davidson_convergence = 0.00001         # Convergence threshold for the residuals in Davidson method
use_casida = false                     # Use full Casida equations; default is TDA
get_all_states = false                 # Calculate all excited states (not just lowest nstates)
```

---

## TD-DFTB Excited States

```toml
[tddftb]
restrict_active_orbitals = false         # Enable orbital restriction (limits calculation to key orbitals)
active_orbital_threshold = 0.2           # Fraction of orbitals included (0.2 = 20% of occupied and virtual orbitals)
save_transition_densities = false        # Save transition density matrices
save_natural_transition_orbitals = false # Save NTOs as .cube files (for visualization)
states_to_analyse = [0, 1]               # Specify which excited states to analyze (e.g., save NTOs)
```

---

## Slater-Koster Parameters

```toml
[slater_koster]
use_external_skf = false          # Use external Slater-Koster files (recommended)
skf_directory = " "               # Path to the directory containing .skf files
```

---

## Parallelization

```toml
[parallelization]
number_of_cores = 1               # Number of CPU cores to use (parallel execution)
```

---

## FMO-LC-TDDFTB Settings

```toml
[fmo_lc_tddftb]
restrict_active_space = true               # Restrict exchange integral calculation to significant transitions only; only TDM matrix elements that are above a threshold will be considered for the exchange evaluation
active_space_threshold_le = 0.0001         # Threshold for including locally excited transitions
active_space_threshold_ct = 0.0001         # Threshold for charge-transfer transitions
n_le = 2                                   # Number of local excited states to consider
n_ct = 1                                   # Number of CT states to include
calculate_all_states = false               # Whether to compute full excitonic Hamiltonian
calculate_ntos = false                     # Enable NTO calculations
calculate_transition_densities = false     # Save transition density matrices
calculate_particle_hole_densities = false  # Save particle/hole density maps
states_to_analyse = [0, 1]                 # Specify which states to analyze
calc_exact_s_sqrt_inv = false              # Compute exact inverse square root of overlap matrix (costly but accurate)
```

---

## Dispersion Corrections (DFT-D3)

```toml
[dispersion]
use_dispersion = false       # Enable Grimme's DFT-D3 dispersion correction; you need to look up the dispersion parameters to the corresponding Slater-Koster files
s6 = 1.0                     # Global scaling factor for dispersion energy
s8 = 0.01                    # Scaling for higher-order dispersion terms
a1 = 0.497                   # Damping function parameter
a2 = 3.622                   # Damping function parameter
```

---

## Monomer Identification

```toml
[identification_config]
atom_coordinates = [[0.0, 0.0, 0.0]]  # Coordinates of a single atom of the monomer for identification in the structure
```

---

## Initial Condition Sampling (Wigner)

```toml
[wigner_config]
n_samples = 50                     # Number of samples to generate (position + velocity)
temperature = 50.0                 # Temperature for sampling (Wigner distribution)
n_cut = 6                          # Number of modes (typically rotational/translation) to exclude from Hessian
save_in_other_path = false         # Save files outside the working directory
wigner_path = " "                  # If saving elsewhere, specify full directory path
write_velocities = true            # Save velocity vectors in output (NumPy format)
```

---

## Create cube files along Ehrenfest trajectory

```toml
[tdm_config]
calculate_nth_step = 10            # Create a cube file for every nth step
total_steps = 1000                 # Set the total number of steps along the trajectory
store_tdm = false                  # Save the TDM as a Numpy file
store_hole_particle = false        # Save the hole and particle density as a cube file
calc_cube = true                   # Compute the cube file of the particle and hole densities
calc_tdm_cube = false              # Compute the cube file of the transition density matrix
use_parallelization = true         # use multithreading for the calculation (high demand of RAM)
```

---

## Strong light-matter interactions

```toml
[polariton]                        # If the jobtype "polariton" is chosen, these options must be considered
e = [[1.0, 1.0, 1.0]]              # activate/deactivate the electric field components of the photon 
p = [[0.0, 0.0, 0.0]]              # electric field polarization of the photon; for x-polarisation, choose [[1.0,0.0,0.0]]
photon_energy = [0.0]              # photon energy
quantized_volume = [1.0]           # quantized volume for the calculation of the light-matter coupling constant g
```