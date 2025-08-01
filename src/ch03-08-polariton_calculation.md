# Strong light-matter interactions
Here, we present an example *dialect.toml* configuration for the calculation of the polaritonic excited states in the framework of FMO-LC-TDDFTB.

### dialect.toml
```toml
jobtype = "polariton"
verbose = 0

[tight_binding]
use_dftb = true
use_xtb1 = false
use_gaussian_gamma = false
use_shell_resolved_gamma = false

[fmo]
fmo = true
vdw_scaling = 2.0

[scf]
scf_max_cycles = 250
scf_charge_conv = 1.0e-8
scf_energy_conv = 1.0e-8

[lc]
long_range_correction = true
long_range_radius = 3.33333333333333

[excited]
calculate_excited_states = true
nstates = 600
davidson_iterations = 100
davidson_subspace_multiplier = 10
davidson_convergence = 0.00001
use_casida = false
get_all_states = false

[tddftb]
restrict_active_orbitals = false
active_orbital_threshold = 0.2
save_transition_densities = false
save_natural_transition_orbitals = false
states_to_analyse = [0, 1]

[slater_koster]
use_external_skf = true
skf_directory = "/Users/einseler/work/slater_koster_files/ob2-1-1/split"

[parallelization]
number_of_cores = 4

[fmo_lc_tddftb]
restrict_active_space = true
active_space_threshold_le = 0.0001
active_space_threshold_ct = 0.0001
n_le = 2
n_ct = 1
calculate_all_states = false
calculate_ntos = false
calculate_transition_densities = false
calculate_particle_hole_densities = false
states_to_analyse = [0, 1]
calc_exact_s_sqrt_inv = false

[dispersion]
use_dispersion = false
s6 = 1.0
s8 = 0.01
a1 = 0.497
a2 = 3.622

[polariton]
e = [[1.0, 1.0, 1.0]]
p = [[0.0, 1.0, 0.0]]
quantized_volume = [10000000]
photon_energy = [0.1838950000382341]
```