# Kicad Build For Linux Guideline

This is a guideline how to build Kicad for Ununtu:

```
Distributor ID: Ubuntu
Description:    Ubuntu 22.04.3 LTS
Release:        22.04
Codename:       jammy
```

# Prerequisites

```
$ sudo apt install build-essential g++ libxmu-dev libiodbc2-dev libsecret-1-dev unixodbc-dev doxygen swig
$ sudo apt install tcllib tklib tcl-dev tk-dev libfreetype-dev libx11-dev libgl1-mesa-dev libfreeimage-dev
$ sudo apt install apidjson-dev libdraco-dev libglew-dev libglm-dev libglu1-mesa-dev freeglut3 freeglut3-dev
$ sudo apt install libcairo2-dev libcurl4-gnutls-dev libfreeimage-dev libnanomsg-dev libgtk-3-dev

```

# Build Open CASCADE Dependencies

```
$ git clone git@github.com:kamejoko80/oneTBB.git
$ cd oneTBB
$ mkdir build && cd build
$ cmake ../
$ make -j
$ sudo make install
```

```
$ wget https://www.vtk.org/files/release/9.3/VTK-9.3.0.tar.gz
$ tar -xvf VTK-9.3.0.tar.gz
$ cd VTK-9.3.0
$ mkdir build && cd Build
$ cmake ../
$ make -j
$ sudo make install
```

# Build Kicad Dependencies

```
$ git clone https://github.com/Open-Cascade-SAS/OCCT.git
$ cd OCCT
$ git checkout V7_5_0
$ mkdir build && cd build
$ sudo cmake ../
$ sudo make -j
$ sudo make install
```

```
$ git clone git@github.com:kamejoko80/ngspice.git
$ cd ngspice
$ ./autogen.sh
$ mkdir build && cd build
$ ../configure --with-ngshared
$ make -j
$ sudo make install
```

```
$ git clone https://github.com/google/protobuf.git
$ cd protobuf
$ git submodule update --init --recursive
$ mkdir build && cd build
$ cmake ../
$ make -j
$ sudo make install
```

Build wxWidgets following https://wiki.wxwidgets.org/Compiling_and_getting_started

```
$ wget https://github.com/wxWidgets/wxWidgets/releases/download/v3.2.5/wxWidgets-3.2.5.tar.bz2
$ tar -xvf wxWidgets-3.2.5.tar.bz2
$ cd wxWidgets-3.2.5
$ mkdir gtk-build && cd gtk-build
$ ../configure --with-opengl --with-gtk=3
$ make -j
$ sudo make install
```

```
$ pip install -U wxPython
```

# Build Kicad

```
$ git clone https://gitlab.com/jeffwheeler/kicad.git
$ cd kicad
$ git checkout add_cadence_allegro_importer
$ mkdir -p build/release
$ cd build/release
$ cmake -DCMAKE_BUILD_TYPE=RelWithDebInfo -DKICAD_USE_EGL=yes ../../
$ make -j
```

# To Run Kicad Without Installation

```
$ export KICAD_RUN_FROM_BUILD_DIR=$PWD/build/release
$ cd build/release/kicad
$ ./kicad
```
