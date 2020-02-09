# wxFormBuilder [![Build Status](https://travis-ci.org/wxFormBuilder/wxFormBuilder.svg?branch=master)](https://travis-ci.org/wxFormBuilder/wxFormBuilder)

## Download Binaries

* [GitHub Releases](https://github.com/wxFormBuilder/wxFormBuilder/releases)

## Install From Source

### Windows (MingW-W64-builds)

Install [MingW-W64-builds](http://www.mingw-w64.org/doku.php/download/mingw-builds) and run the following inside a MinGW 32 bit shell:

```sh
set MINGW_HOME=<your-mingw-w64>\i686-8.1.0-win32-dwarf-rt_v6-rev0\mingw32
set CPLUS_INCLUDE_PATH=%MINGW_HOME%\include
set LIBRARY_PATH=%MINGW_HOME%\lib
set WXWIN=<your-wxWidgets>

git clone --recursive --depth=1 https://github.com/wxFormBuilder/wxFormBuilder
cd wxFormBuilder
cmd.exe /C "create_build_files5.bat --disable-monolithic --force-wx-config --wx-version=3.1"
cd build/3.1/gmake
mingw32-make config=release
```

Run:

```sh
cd ../../../output/
./wxFormBuilder.exe
```

### Windows (MSYS2)

Install [MSYS2](http://msys2.github.io/) and run the following inside a MinGW 32 bit shell:

```sh
pacman -S --needed mingw-w64-i686-wxWidgets git make mingw-w64-i686-binutils mingw-w64-i686-gcc mingw-w64-i686-boost
git clone --recursive --depth=1 https://github.com/wxFormBuilder/wxFormBuilder
cd wxFormBuilder
cmd.exe /C "create_build_files4.bat --wx-root=/mingw32/bin --force-wx-config --disable-mediactrl"
ln -s /mingw32/include/binutils/bfd.h /mingw32/include/bfd.h
ln -s /mingw32/include/binutils/bfd_stdint.h /mingw32/include/bfd_stdint.h
ln -s /mingw32/include/binutils/diagnostics.h /mingw32/include/diagnostics.h
ln -s /mingw32/include/binutils/symcat.h /mingw32/include/symcat.h
ln -s /mingw32/lib/binutils/libbfd.a /mingw32/lib/libbfd.a
ln -s /mingw32/lib/binutils/libiberty.a /mingw32/lib/libiberty.a
cd build/3.0/gmake
sed 's!\$(LDFLAGS) \$(RESOURCES) \$(ARCH) \$(LIBS)!\$(LIBS) \$(LDFLAGS) \$(RESOURCES) \$(ARCH)!g' *.make -i
sed 's!-lbfd!-lbfd -lz!g' *.make -i
make config=release
```

Run:

```sh
cd ../../../output/
./wxFormBuilder.exe
```

### Linux

Pre-requisites for Ubuntu:

```sh
sudo apt install libwxgtk3.0-dev libwxgtk-media3.0-dev meson
```

Pre-requisites for Arch Linux:

```sh
sudo pacman -Syu --needed meson wxgtk2
```

Build and run:

```sh
git clone --recursive --depth=1 https://github.com/wxFormBuilder/wxFormBuilder
cd wxFormBuilder
meson _build --prefix $PWD/_install
ninja -C _build install
./_install/bin/wxformbuilder
```

### macOS

Pre-requisites for macOS can be installed via [Homebrew](https://brew.sh/):

```sh
brew install wxmac boost dylibbundler make
```

Note: Building with Xcode currently does not work without issues (see [issue #247](https://github.com/wxFormBuilder/wxFormBuilder/issues/247)). Therefore it is recommended to build with GNU make like as described below:

```sh
git clone --recursive --depth=1 https://github.com/wxFormBuilder/wxFormBuilder
cd wxFormBuilder
./create_build_files4.sh
cd build/3.0/gmake
make config=release
```

Run:

```sh
cd ../../../output/
open wxFormBuilder.app
```
