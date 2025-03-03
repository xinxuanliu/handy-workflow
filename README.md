# handy-workflow
Diverse handy workflow

## macOS

### Install R using asdf on macOS (2025-03-03)

Here are the steps of: using the multiple versions manager asdf to install R on macOS.

1. Install [Homebrew](https://brew.sh/) and [asdf](https://asdf-vm.com/guide/getting-started.html).  
2. Install R (version 4.4.3 or similar):  
   *Input in terminal (run twice to ensure everything is installed):*
   ```
   brew install gcc pcre2 xz readline jpeg libpng pkgconfig libtiff zlib texinfo openblas
   sudo brew install --cask xquartz basictex
   ```
   *Add to ~/.zshrc:*
   ```
   # For compilers to find openblas
   export LDFLAGS="-L/usr/local/opt/openblas/lib"
   export CPPFLAGS="-I/usr/local/opt/openblas/include"
   
   # For pkg-config to find openblas
   export PKG_CONFIG_PATH="/usr/local/opt/openblas/lib/pkgconfig"
   ```
   *Reopen terminal, input (change 4.4.3 to your version):*
   ```
   asdf plugin add r https://github.com/asdf-community/asdf-r.git
   R_EXTRA_CONFIGURE_OPTIONS='--enable-R-shlib --enable-memory-profiling --x-includes=/opt/X11/include --x-libraries=/opt/X11/lib --with-blas --with-lapack' asdf install r 4.4.3
   ```
   *Optional, set global default R version in .tool-versions file in home directory:*
   ```
   asdf set -u r 4.4.3
   ```
   Ref:
   ```
   https://cran.r-project.org/doc/manuals/r-release/R-admin.html#macOS
   https://github.com/asdf-community/asdf-r
   ```


## Acknowledgements
  - Developers of tools and softwares mentioned above
  - You
