# DFTB ground state calculation
Here, we show example *dialect.toml* file configurations for ground state calculations using various DFTB methods.

## DFTB2
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
multiplicity = 1 # As of now, only singlets are supported

[lc]
long_range_correction = false
long_range_radius = 3.03

[scf]
scf_max_cycles = 250
scf_charge_conv = 1.0e-8
scf_energy_conv = 1.0e-8

[slater_koster]
use_external_skf = true
skf_directory = "/path/to/slater_koster_files/mio-1-1"

[parallelization]
number_of_cores = 1

[dispersion]
use_dispersion = false
s6 = 1.0
s8 = 0.01
a1 = 0.497
a2 = 3.622
```

## LC-DFTB2
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
long_range_correction = true # request long-range correction
long_range_radius = 3.333333 # set the long-range radius -> R_{lc} = 1/omega

[slater_koster]
use_external_skf = true
skf_directory = "/path/to/slater_koster_files/ob2-1-1/split"

[parallelization]
number_of_cores = 1

[dispersion]
use_dispersion = false
s6 = 1.0
s8 = 0.01
a1 = 0.497
a2 = 3.622
```

## DFTB3
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

[lc]
long_range_correction = false
long_range_radius = 3.03

[scf]
scf_max_cycles = 250
scf_charge_conv = 1.0e-8
scf_energy_conv = 1.0e-8

[dftb3]
use_dftb3 = true
use_gamma_damping = false
hubbard_derivatives = [-0.1857, -0.1492] # from the element with the lowest atomic number to the highest

[slater_koster]
use_external_skf = true
skf_directory = "/path/to/work/slater_koster_files/3ob-3-1"

[parallelization]
number_of_cores = 1

[dispersion]
use_dispersion = false
s6 = 1.0
s8 = 0.01
a1 = 0.497
a2 = 3.622
```