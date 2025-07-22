# DFTB dynamics simulation
Here, we show example *dialect.toml* and *dynamics.toml* file configurations for the simulation of molecular dynamics using DFTB methods.

## Ground state dynamics
### dialect.toml
```toml
jobtype = "dynamics"
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

### dynamics.toml
```toml
nstep = 100 # Number of steps
stepsize = 0.1 # stepsize in fs
restart_flag = false # request restart of the dynamcis simulation
initial_state = [0] # initial state for the simulation
nstates = 1 # Number of electronic states
gs_dynamic = true # Flag for ground state dynamics
use_surface_hopping = false
use_ehrenfest = false 
load_velocities_from_file = false # Read initial velocities from the file velocities.npy
use_boltzmann_velocities = true # Sample initial velocities from Maxwell-Boltzmann distribution

[thermostat_config]
use_thermostat = false # Use a thermostat, here Berendsen
temperature = 300.0 
time_coupling = 50.0 # time coupling constant of the thermostat

[print_config]
print_restart = true # write a restart file
print_coordinates = true # write the coordinates in a trajetory file, dynamics.xyz
print_energies = true # write the energies to a file
print_temperature = true # write the temperature to a file
```

## Excited state surface hopping dynamics
### dialect.toml
```toml
jobtype = "dynamics"
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
calculate_excited_states = true
nstates = 10
davidson_iterations = 100
davidson_subspace_multiplier = 10
davidson_convergence = 0.00001
use_casida = false
get_all_states = false

[tddftb]
restrict_active_orbitals = false
active_orbital_threshold = 0.2
save_transition_densities = false
states_to_analyse = [0, 1]

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

### dynamics.toml
```toml
nstep = 100
stepsize = 0.1
restart_flag = false
initial_state = [2]
nstates = 8
gs_dynamic = false
use_surface_hopping = true # Do a surface hopping molecular dynamics simulation
use_ehrenfest = false # request the use of the Ehrenfest method
load_velocities_from_file = false
use_boltzmann_velocities = true

[hopping_config]
force_switch_to_gs = true # In TDDFTB, the conical intersection between the ground state and the excited states is only represented by a simple crossing instead of a cone. This option forces the trajectory to hop to the ground state if the difference in potential energy is below a certain threshold.
decoherence_correction = true # Use a decoherence correction
use_rk_integration = false # integrate the differential equation of the expansion coefficients with Runge-Kutta
use_local_diabatisation = true # Use the local diabatisation for the surface hopping dynamics to avoid strongly peaked nonadiabatic coupling values
use_rescaling_at_frustrated_hop = true # rescale velocities at frustrated hops
integration_steps = 1000 # integration steps for the Runge-Kutta routine

[nonadibatic_config]
use_nacv_couplings = true # Use nonadiabatic coupling vectors for the surface hopping procedure
use_nact_couplings = false # Use the scalar coupling for the surface hopping dynamics

[thermostat_config]
use_thermostat = false # use a Berendsen thermostat
temperature = 300.0 # Temperature in Kelvin
time_coupling = 50.0 # time coupling constant of the Berendsen thermostat

[print_config]
print_restart = true # write a restart file from where a dynamics calculation can be restarted
print_coordinates = true # write the coordinates to the file "dynamics.xyz"
print_energies = true # write the energies to a file
print_temperature = true # write the temperature to a file
print_state = true # write the state for the surface hopping method for each geometry along the trajectory to a file
```