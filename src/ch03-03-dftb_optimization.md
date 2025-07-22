# DFTB geometry optimization
Here, we show example *dialect.toml* file configurations for the geometry optimization of the ground and excited state.

## Ground state
```toml
jobtype = "opt"
verbose = 0

[tight_binding]
use_dftb = true 
use_xtb1 = false   
use_gaussian_gamma = false  
use_shell_resolved_gamma = false 

[fmo]
fmo = false
vdw_scaling = 2.0

[mol]
charge = 0
multiplicity = 1

[lc]
long_range_correction = false
long_range_radius = 3.03

[scf]
scf_max_cycles = 250
scf_charge_conv = 1.0e-8
scf_energy_conv = 1.0e-8

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
```

## Excited state
```toml
jobtype = "opt"
verbose = 0

[tight_binding]
use_dftb = true 
use_xtb1 = false   
use_gaussian_gamma = false  
use_shell_resolved_gamma = false 

[fmo]
fmo = false
vdw_scaling = 2.0

[lc]
long_range_correction = false
long_range_radius = 3.03

[scf]
scf_max_cycles = 250
scf_charge_conv = 1.0e-8
scf_energy_conv = 1.0e-8

[opt]
state_to_optimize = 1
geom_opt_max_cycles = 500
geom_opt_tol_displacement = 1.0
geom_opt_tol_gradient = 1.0
geom_opt_tol_energy = 1.0e-1
use_bfgs = true
use_line_search = true

[excited]
calculate_excited_states = true
nstates = 10
davidson_iterations = 100
davidson_subspace_multiplier = 10
davidson_convergence = 0.00001
use_casida = false
get_all_states = false

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
```