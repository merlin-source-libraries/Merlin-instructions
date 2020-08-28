# Merlin-instructions
Installation instructions and usage recommendations of Merlin C++ source libraries

### Installation instructions

Each Merlin library provide a simple _install.sh_ script to make the installation easier. The script will:

- Expect to be called from the repository
- Expect one argument to specify the install directory
- Create the installation directory (if needed)
- Create _include_ and _lib_ folders (if needed) in the install directory
- Copy the library headers into the proper install location
- Generate (requires GCC g++) the shared object (.so) into the proper install location (except for template-only header-only libraries)

**Note:** The _install.sh_ script may require sudo permission rights depending on the install directory location/permissions.

**Example:**
```
$ cd /path_to/repository/
$ sudo ./install.sh /opt/Merlin/
```

### Usage recommendations

When using a Merlin library in one's project, it may be inconvenient to have to specify the Merlin _include_ and _lib_ directories paths in the compilation command (e.g. `-I/opt/Merlin/include` and `-L/opt/Merlin/lib`).

We would advise to edit the _.bashrc_ file (under Linux) and set the `CPLUS_INCLUDE_PATH` and `LIBRARY_PATH` environment variables (at least for GCC g++) to let respectively the preprocessor and the linker find the Merlin installation without explicit compilation arguments anymore.

Moreover it is also recommended to set the `LD_LIBRARY_PATH` environment variable in order to let the loader find the shared libraries at runtime.

**Example:**

<sub>_.bashrc (append the following bash instructions)_</sub>
```
export MERLIN_INSTALL_DIR=/opt/Merlin/
export CPLUS_INCLUDE_PATH=${MERLIN_INSTALL_DIR}include:$CPLUS_INCLUDE_PATH
export LIBRARY_PATH=${MERLIN_INSTALL_DIR}lib:$LIBRARY_PATH
export LD_LIBRARY_PATH=${MERLIN_INSTALL_DIR}lib:$LD_LIBRARY_PATH
```

**Note:** Adding the extra environment variable `MERLIN_INSTALL_DIR` could be useful to standardize the installation of Merlin libraries as `./install.sh $MERLIN_INSTALL_DIR`.
