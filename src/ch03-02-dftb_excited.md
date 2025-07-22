# DFTB excited-state calculation
Here, we show an example *dialect.toml* file configuration for excited-state calculations using LC-DFTB.

```toml
jobtype = "sp"
verbose = 0

[tight_binding]
use_dftb = true 
use_xtb1 = false   
use_gaussian_gamma = false  
use_shell_resolved_gamma = false 

[mol]
charge = 0
multiplicity = 1

[scf]
scf_max_cycles = 250
scf_charge_conv = 1.0e-8
scf_energy_conv = 1.0e-8

[lc]
long_range_correction = true
long_range_radius = 3.333333

[excited]
calculate_excited_states = true # request excited states
nstates = 10 # number of excited states
davidson_iterations = 100 # Maximum number of iterations for the Davidson algorithm
davidson_subspace_multiplier = 10 # Sets the maximum number of guess vectors for the Davidson algorithm as: 10 * NrExcitations -> Here, it would result in a maximum subspace of 100
davidson_convergence = 0.00001 # Tolerance threshold for the residuals of the Davidson alogrithm
use_casida = false # if false, only TDA is performed
get_all_states = false # if requested, the full excited state manifold of singly excited singlet states is calculated -> Builds full A matrix 

[tddftb]
restrict_active_orbitals = false # restrict the number of orbitals for the excited state calculation
active_orbital_threshold = 0.5 # 50% of the occupied and virtual orbitals are used for the excited state calculation
save_transition_densities = false # save transition densities to npy file
save_natural_transition_orbitals = true # request NTOs if desired
states_to_analyse = [0, 1] # states for the calculation of transition densities and NTOs

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