# handy-workflow
Diverse handy workflow

## macOS

### Install R using asdf on macOS

Here are the steps of: using the multiple versions manager asdf to install R on macOS (2025-03-03).

1. Install [Homebrew](https://brew.sh/) and [asdf](https://asdf-vm.com/guide/getting-started.html).  
2. Install R (version 4.4.3 or similar):
   - Run below in terminal twice to ensure everything is installed (may require your system password):  
     *You can just install gfortran instead of gcc, see https://cran.r-project.org/doc/manuals/r-release/R-admin.html#Fortran-compilers.*
   ```
   brew install gcc pcre2 xz readline jpeg libpng pkgconfig libtiff zlib texinfo openblas
   brew install --cask xquartz basictex
   ```
   - Optionally, enable OpenMP refer to [here](#enable-openmp-on-macos).
   - Enable OpenBLAS, add to ~/.zshrc (if OpenBLAS is installed manually or via a package manager other than Homebrew, update the path as needed):
   ```
   # Enable OpenBLAS
   export LDFLAGS="${LDFLAGS} -L/usr/local/opt/openblas/lib"
   export CPPFLAGS="${CPPFLAGS} -I/usr/local/opt/openblas/include"
   export PKG_CONFIG_PATH="${PKG_CONFIG_PATH} /usr/local/opt/openblas/lib/pkgconfig"
   ```
   - Reopen terminal, run (change 4.4.3 to your version):
   ```
   asdf plugin add r https://github.com/asdf-community/asdf-r.git
   R_EXTRA_CONFIGURE_OPTIONS='--enable-R-shlib --enable-memory-profiling --x-includes=/opt/X11/include --x-libraries=/opt/X11/lib --with-blas --with-lapack' asdf install r 4.4.3
   ```
   - Optionally, set global default R version in ~/.tool-versions, run in terminal:
   ```
   asdf set -u r 4.4.3
   ```
   - Optionally, use asdf R in RStudio (assuming no additional R installations exist), run in terminal:
   ```
   sudo ln -s ~/.asdf/shims/R /usr/local/bin/R
   ```
   - Optionally, check if OpenBLAS is correctly configured, run in R:
   ```
   sessionInfo()
   ```
Ref:
```
https://cran.r-project.org/doc/manuals/r-release/R-admin.html#macOS
https://github.com/asdf-community/asdf-r
```


### Enable OpenMP on macOS

2025-03-03

1. Install Xcode Command Line Tools (CLT):
   - Run in terminal:
   ```
   xcode-select --install
   ```
2. Check Xcode CLT version:
   - Run in terminal:
   ```
   pkgutil --pkg-info=com.apple.pkg.CLTools_Executables
   ```
3. Copy the link of "libomp run-time Release file" corresponding to your version from the table in: <https://mac.r-project.org/openmp/>.  
   For example: https://mac.r-project.org/openmp/openmp-10.0.0-darwin17-Release.tar.gz.
   - Run in terminal (change to your link and file name, refer to the next step if an error occurs):
   ```
   curl -O https://mac.r-project.org/openmp/openmp-10.0.0-darwin17-Release.tar.gz
   sudo tar fvxz openmp-10.0.0-darwin17-Release.tar.gz -C /
   ```
   - Even if you encounter an error when running above code, proceed to the next step if the files below exist (so to uninstall, just remove them):
   ```
   ls /usr/local/lib/libomp.dylib
   ls /usr/local/include/ompt.h
   ls /usr/local/include/omp.h
   ls /usr/local/include/omp-tools.h
   # Release 19.1.0 adds a new file:
   ls /usr/local/include/ompx.h
   ```
   - Add below to ~/.zshrc, then reopen terminal or software to use OpenMP:
   ```
   # Enable OpenMP
   export LDFLAGS="${LDFLAGS} -lomp"
   export CPPFLAGS="${CPPFLAGS} -Xclang -fopenmp"
   ```
Ref:
```
https://mac.r-project.org/openmp
```


### Create a RAM disk on macOS

2025-04-16

1. Calculate the size of the disk:
   - Size is the number of 512-byte blocks contained in the RAM disk.
   - Size = 1 means 512 B, size = 2048 means 1 MiB, size = 2097152 means 1 GiB.
2. Substitute name and size you want of the disk in examples below:  
   *The touch command at the end tells Spotlight not to needlessly index it.*
   - Create a RAM disk of 2 GiB (size = 4194304) named RAMDisk1 in APFS format, run in terminal:
   ```
   diskutil apfs create $(hdiutil attach -nomount ram://4194304) RAMDisk1 && touch /Volumes/RAMDisk1/.metadata_never_index
   ```
   - Create a RAM disk of 2 GiB (size = 4194304) named RAMDisk2 in HFS+ format, run in terminal:
   ```
   diskutil erasevolume HFS+ RAMDisk2 `hdiutil attach -nomount ram://4194304` && touch /Volumes/RAMDisk2/.metadata_never_index
   ```
3. To release the RAM, select one from the ways below:  
   *Attention! No data can survive after releasing the RAM.*
   - Eject the RAM disk.
   - Reboot computer.
   - Shutdown computer.

Ref:
```
https://superuser.com/questions/1480144/creating-a-ram-disk-on-macos
```


## Acknowledgements
  - Developers of tools and softwares mentioned above
  - You
