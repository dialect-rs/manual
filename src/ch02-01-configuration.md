# Program settings
To configure the settings for a calculation using the __DIALECT__ program, the file __dialect.toml__ has to be created. You can either create the file yourself or you can run the program in a directory without the configuration file:
```sh
/your/path/to/DIALECT/dialect file.xyz
```
The __dialect.toml__ will then be created using the standard values of the program. 
The settings of the file dialect.toml are explained in the following sections.
## General settings
```toml
jobtype = "sp"
fmo = false
verbose = 0
```
### jobtype
You can choose between "sp" for a DFTB or FMO-LC-DFTB calculation or "density" for the calculation of a given density in the AO basis on a grid.
### fmo 
If you want to do a FMO-DFTB calculation, set fmo=true.
### verbose
Concerns the verbosity of the output. Values from -2 to 2 are possible. Higher values result in a much more detailed output.
## [mol] config
```toml
[mol]
charge = 0
multiplicity = 1
```
You can change the charge and the multiplicity of the molecule. But at this point in time, the program only supports closed shell configurations!
## [scf] config
The convergence settings of the self-consistent charge (SCC) routine are defined here. 
```toml
[scf]
scf_max_cycles = 250
scf_charge_conv = 0.00001
scf_energy_conv = 0.00001
```
### scf_max_cycles
Maximum number of iterations for the SCC routine
### scf_charge_conv 
Convergence criterium of the SCC routine. It concerns the charge difference to the previous iteration.
### scf_energy_conv
Convergence criterium of the SCC routine. It concerns the energy difference to the previous iteration.
## [lc] config
Here, you can turn the long-rang correction on and set the long-range radius. Be aware that a FMO calculation only works with an activated long-range correction.
```toml
[lc]
long_range_correction = true
long_range_radius = 3.03
```
## [excited] config
```toml
[excited]
nstates = 10
davidson_iterations = 100
davidson_subspace_multiplier = 10
```
### nstates
Number of requested excites states.
### davidson_iterations
Maximum number of iterations for the Davidson routine.
### davidson_subspace_multiplier
Maximum scaling factor of the dimension for the guess vectors of the Davidson algorithm. It is multiplied with the number of requested excited states.
## [tda_dftb] config
```toml
[tda_dftb]
restrict_active_orbitals = false
active_orbital_threshold = 0.2
save_transition_densities = false
states_to_analyse = [0, 1]
```
Settings concerning a normal TDA-TDDFTB calculation
### restrict_active_orbitals
Reduce the number of occupied and virtual orbitals involved during the TDDFTB calulation.
### active_orbital_threshold
Set the fraction of the full orbital space
### save_transition_densities
Save the transition density matrix in AO basis for the requested excited states.
### states_to_analyse
Select the states for which you want to calculate and save the transition density matrices.
## [slater_koster] config
```toml
[slater_koster]
use_external_skf = false
skf_directory = " "
```
### use_external_skf
Use Slater-Koster parameters from external source.
### skf_directory
Specify the path to the SKF-files. "/path/to/SKF/"
## [parallelization] config
```toml
[parallelization]
number_of_cores = 1
```
### number_of_cores
Use the specified number of processor cores for the calculation. It only affects a FMO-DFTB calculation
## [fmo_lc_tddftb] config
```toml
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
```
Settings for the excited state calculation using the FMO-LC-TDDFTB method
### restrict_active_space
Calculate only relevant transitions between orbitals for the exchange part of the couplings between the LE and CT states.
### active_space_treshold_le 
Threshold for the one electron transition density matrices of the LE states.
### active_space_treshold_ct
Threshold for the one electron transition density matrices of the CT states.
### n_le
Number of locally excited states for each monomer fragment.
### n_ct
Number of charge-transfer states for each pair fragment.
### calculate_all_states
Do a full diagonalization of the excitonic Hamiltonian instead of the Davidson routine.
### calculate_ntos
Calculate the natural transition orbitals for the specified excited states. They will be stored as molden files, which can be viewed in jmol.
### calculate_transition_densities
Calculate the transition density matrices in AO basis for the specified excited states. They will be stored as binary numpy files.
### calculate_particle_hole_densities
Calculate the particle and hole densities for the specified excited states. They will be stored as binary numpy files.
### states_to_analyze
List of the excited states for which the ntos or densities will be calculated.
## [density] config
```toml
[density]
path_to_density = " "
points_per_bohr = 2.0
threshold = 0.0001
use_block_implementation = true
n_blocks = 1
```
Settings regarding the calculation of a density in AO basis on the grid, which will be stored as a cube file.
### path_to_density
Specify the full path to the density file: /path/to/density/density.npy
### points_per_bohr
Number of grid points per bohr
### threshold
Relative threshold of the matrix elements of the density, which will be used in the calculation of the cube file.
### use_block_implementation
Should be used if a large molecular systems is considered. Otherwise, the data of the basis functions, which are going to be evaluated on the complete grid, wont fit into the RAM of your system.
### n_blocks
The number of blocks the density matrix will be partitioned into. 

