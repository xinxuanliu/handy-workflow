# handy-workflow
Diverse handy workflow

## macOS

### Install R using asdf on macOS  !NOT DONE!

Here are the steps of: using the multiple versions manager asdf to install R on macOS.

1. Install [Homebrew](https://brew.sh/) and [asdf](https://asdf-vm.com/guide/getting-started.html).  
2. Install R (for R version 4.4.2 or similar).  
   *Input in terminal:*
   ```
   brew install gcc pcre2 xz readline jpeg libpng pkgconfig libtiff zlib libxt openblas
   ```
   *Add to ~/.zshrc:*
   ```
   # For compilers to find openblas
   export LDFLAGS="-L/usr/local/opt/openblas/lib"
   export CPPFLAGS="-I/usr/local/opt/openblas/include"
   
   # For pkg-config to find openblas
   export PKG_CONFIG_PATH="/usr/local/opt/openblas/lib/pkgconfig"
   ```
   *Reopen terminal, input:*
   ```
   asdf plugin add r https://github.com/asdf-community/asdf-r.git
   R_EXTRA_CONFIGURE_OPTIONS='--enable-R-shlib --enable-memory-profiling --with-blas --with-lapack' asdf install r 4.4.3
   ```
   Ref:
   ```
   https://cran.r-project.org/doc/manuals/r-release/R-admin.html#macOS. (2024-10-31)
   https://github.com/asdf-community/asdf-r (2025-03-02)
   ```


## Acknowledgments
  - Developers of tools and softwares mentioned above
  - You
