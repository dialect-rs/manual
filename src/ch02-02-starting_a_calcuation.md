# Calling the program
If you have the __DIALECT__ executable in your `PATH`, you can simply start a calculation using
```sh
dialect file.xyz
```
Otherwise you would have to call the program using the full path to the DIALECT binary
```sh
/your/path/to/DIALECT/dialect file.xyz
```
Normally the output of the program is printed to the console. To save the output to a file, use:
```sh
dialect file.xyz &> output.dat
```
If you intend to use the built in DFTB parameterization, you are required to set the `DIALECT_SRC_DIR` to the folder containing the source files of the program:
```sh
export DIALECT_SRC_DIR=/your/path/to/DIALECT
```
