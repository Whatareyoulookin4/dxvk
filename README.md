# DXVK

Provides a Vulkan-based implementation of DXGI and D3D11 in order to run 3D applications on Linux using Wine.

For the current status of the project, please refer to the [project wiki](https://github.com/doitsujin/dxvk/wiki).

## Build instructions

### Requirements:
- [wine-staging](https://wine-staging.com/) for Vulkan support
- [Meson](http://mesonbuild.com/) build system
- [MinGW64](http://mingw-w64.org/) compiler and headers
- [SDL2](https://www.libsdl.org/) headers and DLL

### Building DLLs
Inside the dxvk directory, run:
```
meson --cross-file build-win64.txt build.w64
cd build.w64
meson configure -Dprefix=/your/directory
ninja
ninja install
```

Both `dxgi.dll` and `d3d11.dll`as well as some demo executables will be located in `/your/directory/bin`. 32-bit builds are currently not supported.

## How to use
In order to run `executable.exe` with DXVK,
* Copy `dxgi.dll`, `d3d11.dll` and `SDL2.dll` into the same directory as the executable
* Run `WINEDLLOVERRIDES=d3d11,dxgi=n wine executable.exe`

DXVK will create a file `dxgi.log` in the current working directory and may print out messages to stderr.

### Environment variables
The behaviour of DXVK can be modified with environment variables.

- `DXVK_SHADER_DUMP_PATH=directory` Writes all DXBC and SPIR-V shaders to the given directory
- `DXVK_SHADER_READS_PATH=directory` Reads SPIR-V shaders from the given directory instead of compiling the DXBC shader.
- `DXVK_DEBUG_LAYERS=1` Enables Vulkan debug layers. Highly recommended for troubleshooting and debugging purposes.