# Love2d for Vita

This is a WIP attempt to get the 2d game engine Love to work on the Playstation Vita. It currently does not work yet.

## Building

Before building is possible, use vita-makepkg to build and vdpm to install all VITABUILDs in ``packages``.

Once this is done, building love can be done with:
```
mkdir love/build && cd love/build

cmake \
-DCMAKE_TOOLCHAIN_FILE=$VITASDK/share/vita.toolchain.cmake \
-DFREETYPE_LIBRARY=${VITASDK}/arm-vita-eabi/lib/libfreetype.a \
-DFREETYPE_INCLUDE_DIRS=${VITASDK}/arm-vita-eabi/include/freetype2 \
-DOPENGL_opengl_LIBRARY=${VITASDK}/arm-vita-eabi/lib/libGL.a \
-DOPENGL_INCLUDE_DIR=${VITASDK}/arm-vita-eabi/include/GL \
-DOPENGL_glx_LIBRARY=${VITASDK}/arm-vita-eabi/include/GLUT \
-DMODPLUG_LIBRARY=${VITASDK}/arm-vita-eabi/lib/libmodplug.a \
-DMODPLUG_INCLUDE_DIR=${VITASDK}/arm-vita-eabi/include/libmodplug \
-DOPENAL_LIBRARY=${VITASDK}/arm-vita-eabi/lib/libopenal_stub.a \
-DOPENAL_INCLUDE_DIR=${VITASDK}/arm-vita-eabi/include/AL \
-DSDL2_INCLUDE_DIR=${VITASDK}/arm-vita-eabi/include/SDL2 \
-DLUAJIT_INCLUDE_DIR=${VITASDK}/arm-vita-eabi/include/luajit-2.0 \
..

make
```

Lua-jit can be found here: https://github.com/vitasdk/packages/pull/141

## Changes

Some changes were made to the CMakeLists.txt to make sure enet and lua-sockets are not being included. Networking support is an issue for later. Some additional libraries have also been added for linking. Instead of the included physfs, the system on is used.

An instance of posix_memalign being used has been replaced as well here: https://github.com/sharkwouter/vita-love/blob/42180a974a1ff21d63743a1808c923e2a67028a3/love/src/common/memory.cpp#L41

src/modules/image/magpie lines 315, 376 and 377 had types which didn't match when using std::max.
