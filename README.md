# handy-workflow
Diverse handy workflow

## macOS

### Install R using asdf on macOS

Here are the steps of: using the multiple versions manager asdf to install R on macOS.

1. Install asdf according to <https://asdf-vm.com/guide/getting-started.html>.  
2. Install R (here for R, version 4.4.2 or similar) using [Homebrew](https://brew.sh/).  
   *Input below to terminal. Make sure you have Internet connect.*
   ```
   brew install gcc pcre2 xz readline jpeg libpng pkgconfig libtiff zlib libxt
   asdf plugin-add r https://github.com/asdf-community/asdf-r.git
   R_EXTRA_CONFIGURE_OPTIONS='--enable-R-shlib --enable-memory-profiling' asdf install r <version>
   ```
   Ref:
   ```
   https://cran.r-project.org/doc/manuals/r-release/R-admin.html#macOS. (2024-10-31)
   https://github.com/asdf-community/asdf-r (2025-03-02)
   ```


## Acknowledgments
  - You
  - Everyone
