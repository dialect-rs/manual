# FMO-DFTB ground state calculation
Here, we show an example *dialect.toml* file configuration for a ground state calculation using the (LC-)DFTB2 method.

## DFTB2
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
long_range_correction = false
long_range_radius = 3.333333

[slater_koster]
use_external_skf = true
skf_directory = "/path/to/slater_koster"

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