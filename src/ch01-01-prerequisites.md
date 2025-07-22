# Using pre-compiled binaries
A precompiled binary of DIALECT, which was compiled using github actions, is provided with the release on github.

The use of the pre-compiled binaries requires the installation of certain libraries on your computer.

## GCC
As the pre-complied binaries are dynamically linked against the GCC library, it has to be installed on your system. An example for the installation of GCC on a Debian or Ubuntu machine is shown here.
```bash‚
sudo apt-get install gcc
```
# Compiling the code
If you want to compile the program from source, you need to install additional programs and libraries.
## Rust
Of course you need the Rust programming language itself to compile the code. The installation is explained in 
detail on the [official site](https://www.rust-lang.org/tools/install).
## CMaKe
To compile certain Rust packages, you also need to install cmake.
```bash
sudo apt-get install cmake
```
## Gfortran
In addition, the Gfortran compiler must be installed.
```bash‚
sudo apt-get install gfortran
```
## Open-SSL
You need Open-SSL as some used Rust libraries depend on it. You can follow the guide 
shown [here](https://www.howtoforge.com/tutorial/how-to-install-openssl-from-source-on-linux/) to install Open-SSL on 
linux.  
## Linear Algebra Libraries
To be able to compile and run the __DIALECT__ program, it is necessary to download a linear algebra package as a requirement for the ndarray_linalg rust crate. You can choose between Intel MKL, OPENBLAS or Netlib by changing the features of ndarray_linalg in the Cargo.toml file according to the documentation ([github page](https://github.com/rust-ndarray/ndarray-linalg)). In our experience, the intel MKL library yields the best performance. 

Per default, the Cargo.toml files of DIALECT configure the ndarray_linalg create with "openblas-static", which should download and compile the OPENBLAS library and link it with the DIALECT package.

If you want to use the linear algebra packages that are already installed on your system, you need to change the feature of ndarray_linalg in the Cargo.toml files to "openblas-system", "intel-mkl-system" or "netlib-system".

The instructions for the installation of the libraries are provided in the following section. 

## Installation of LINALG packages

### Intel MKL
If you want to compile DIALECT from source using the intel MKL as the linear algebra package, you will need to install it according to the following steps.

You can just download the MKL library from the [Intel webpage](https://software.intel.com/content/www/us/en/develop/articles/oneapi-standalone-components.html) and after the installation the environment variable $MKLROOT must be set with the `setvars.sh` script, which is located in the root
installation directory of MKL.
```bash
source /path/to/MKL/setvars.sh
```  
In the case of the older versions you have to execute the `mklvars.sh` script that is located
in the installation directory of the MKL Library. 
```bash
source /path/to/MKL/mklvars.sh intel64
```  
### OPENBLAS/Netlib
If you want to use OPENBLAS or netlib as the LINALG library, you need to install the BLAS and LAPACK libraries with the package manager of your operating systems.
```bash
sudo apt-get install libopenblas-dev
sudo apt-get install libblas-dev
sudo apt-get install libatlas-base-dev 
sudo apt-get install liblapack-dev
```

## Mac users
In case of Mac users that have an apple silicon based processor, we recommend the compilation of DIALECT in conjunction with the accelerate framework.

A few changes to the Cargo.toml files are neccessary to compile DIALECT with accelerate:

```toml
ndarray-linalg = { version = "0.16", default-features = false }
blas-src = { version = "0.8", features = ["accelerate"] }
```

In addition, a build.rs file that contains the following line

```rust
fn main() {println!("cargo:rustc-link-lib=framework=Accelerate")}
```
must be created in the src folders of the DIALECT package and the dialect dynamics subpackage in order to use the accelerate framework.