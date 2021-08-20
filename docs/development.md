# Developer Build

To build ZENO, you need:

- GCC 9+ or MSVC 19+, CMake 3.12+, and Python 3.6+ to build ZENO.
- Pybind11, NumPy and PySide2 (Qt for Python) to run ZENO editor.
- (Optional) OpenVDB for building volume nodes; CUDA for GPU nodes.

> Hint: for Python, please try avoid using virtualenv and Conda if possible.
> WSL is also not recommended because of its limited GUI and OpenGL support.

Click links below for detailed setup for each platform:

- [Windows 10](/dev/dev_win10.md)
- [Ubuntu 20.04](/dev/dev_ubuntu20.md)
- [CentOS 7](/dev/dev_centos7.md)
- [Arch Linux](/dev/dev_archlinux.md)

After finishing building, use `run.py` to run ZENO for development! You may click `File -> Open` to play `graphs/LorenzParticleTrail.zsg` to confirm everything is working well :)

## Write your own extension!

See [zenustech/zeno_addon_wizard](https://github.com/zenustech/zeno_addon_wizard) for an example on how to write custom nodes in ZENO.

## Blender addon

Blender user? Be sure to check out [ZenoBlend](https://github.com/zenustech/zenoblend)!
