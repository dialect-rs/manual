# DFTB excited state dynamics initial conditions
Here, we show example *dialect.toml* file configuration for the calculation of initial coordinates and velocities of a surface hopping simulation. 

The jobtype "initial_conditions" first performs a optimization of the geometry, which is followed by the calculation of the ground-state Hessian and concluded by the sampling of a Wigner distribution.

### dialect.toml
```toml
jobtype = "initial_conditions"
verbose = 0

[tight_binding]
use_dftb = true 
use_xtb1 = false   
use_gaussian_gamma = false  
use_shell_resolved_gamma = false 

[scf]
scf_max_cycles = 250
scf_charge_conv = 1.0e-8
scf_energy_conv = 1.0e-8

[lc]
long_range_correction = true
long_range_radius = 3.333333

[opt]
state_to_optimize = 0 # optimize the ground state
geom_opt_max_cycles = 500 # maximum iterations
geom_opt_tol_displacement = 1.0 # geometry displacement tolerance
geom_opt_tol_gradient = 1.0 # gradient tolerance
geom_opt_tol_energy = 1.0e-1 # energy tolerance
use_bfgs = true # employ lbfgs
use_line_search = true # utilize line search

[slater_koster]
use_external_skf = true
skf_directory = "/path/to/skf/files"

[parallelization]
number_of_cores = 1

[dispersion]
use_dispersion = false
s6 = 1.0
s8 = 0.01
a1 = 0.497
a2 = 3.622

[wigner_config]
n_samples = 50                     # Number of samples to generate (position + velocity)
temperature = 50.0                 # Temperature for sampling (Wigner distribution)
n_cut = 6                          # Number of modes (typically rotational/translation) to exclude from Hessian
save_in_other_path = false         # Save files outside the working directory?
wigner_path = " "                  # If saving elsewhere, specify full directory path
write_velocities = true            # Save velocity vectors in output (NumPy format)
```