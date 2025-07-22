# FMO-DFTB excited state calculation
Here, we show an example *dialect.toml* file configuration for an excited state calculation using the FMO-LC-TDDFTB method.

```toml
jobtype = "sp"
verbose = 0

[tight_binding]
use_dftb = true 
use_xtb1 = false   
use_gaussian_gamma = false  
use_shell_resolved_gamma = false 

[fmo]
fmo = true
vdw_scaling = 2.0

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
calculate_excited_states = true
nstates = 100
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

[fmo_lc_tddftb]
restrict_active_space = true # Restricts the transition density matrix elements for the calculation of the exchange interactions between LE and CT states 
active_space_threshold_le = 0.0001 # threshold for the tdm matrix for LE interactions
active_space_threshold_ct = 0.0001 # threshold for the tdm matrix for CT interactions
n_le = 3 # Number of requested LE states for each fragment
n_ct = 1 # Number of requested CT states for each fragment pair
calculate_all_states = false # Calculate all excited states of the excitonic Hamiltonian
calculate_ntos = false # Calculate NTOs, which are then saved in a molden file that works with jmol
calculate_transition_densities = false # request the calculation of transition densities
calculate_particle_hole_densities = false # request the calculation of particle hole densities
states_to_analyse = [0, 1] # states for the NTO generation
calc_exact_s_sqrt_inv = false # request the exact calculation of the S^-1/2 matrix

[dispersion]
use_dispersion = false
s6 = 1.0
s8 = 0.01
a1 = 0.497
a2 = 3.622
```