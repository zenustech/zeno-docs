# Introduction

[![NPM](https://img.shields.io/npm/v/docsify-themeable.svg?style=flat-square)](https://www.npmjs.com/package/docsify-themeable)
[![Codacy grade](https://img.shields.io/codacy/grade/860d40719cbd4e0f91e145b87ec7c29a.svg?style=flat-square)](https://www.codacy.com/app/jhildenbiddle/docsify-themeable?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=jhildenbiddle/docsify-themeable&amp;utm_campaign=Badge_Grade)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://github.com/jhildenbiddle/docsify-themeable/blob/master/LICENSE)
[![jsDelivr](https://data.jsdelivr.com/v1/package/npm/docsify-themeable/badge)](https://www.jsdelivr.com/package/npm/docsify-themeable)
[![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?url=https%3A%2F%2Fgithub.com%2Fjhildenbiddle%2Fdocsify-themeable&hashtags=css,docsify,developers,frontend)
<a class="github-button" href="https://github.com/jhildenbiddle/docsify-themeable" data-icon="octicon-star" data-show-count="true" aria-label="Star jhildenbiddle/docsify-themeable on GitHub">Star</a>

Open-source node system framework, to change your algorithmic code into useful tools to create much more complicated simulations!

![rigid3.zsg](/images/rigid3.jpg "arts/rigid3.zsg")

ZENO is an OpenSource, Node based 3D system able to produce cinematic physics effects at High Efficiency, it was designed for large scale simulations and has been tested on complex setups.
Aside of its simulation Tools, ZENO provides necessary visualization nodes for users to import and run simulations if you feel that the current software you are using is too slow.

- [Why a new node system?](/docs/motivation.md)

## Features

Integrated Toolbox, from volumetric geometry process tools (OpenVDB), to state-of-art, commercially robust, highly optimized physics solvers and visualization
nodes, and various VFX and simulation solutions based on our nodes (provided by .zsg file in `graphs/` folder).

## Gallery

![robot hit water](/images/crag_hit_water.gif)

![SuperSonic Flow](/images/shock.gif)


# End-user Installation

## Download binary release

Go to the [release page](https://github.com/zenustech/zeno/releases/), and click Assets -> download `zeno-linux-20xx.x.x.tar.gz`.
Then, extract this archive, and simply run `./launcher` (`launcher.exe` for Windows), then the node editor window will shows up if everything is working well.

## How to play

There are some example graphs in the `graphs/` folder, you may open them in the editor and have fun!
Hint: To run an animation for 100 frames, change the `1` on the top-left of node editor to `100`, then click `Run`.
Also MMB to drag in the node editor, LMB click on sockets to create connections. MMB drag in the viewport to orbit camera, Shift+MMB to pan camera.
More details are available in [our official tutorial](https://zenustech.com/tutorial).

## Bug report

If you find the binary version didn't worked properly or some error message has been thrown on your machine, please let me know by opening an [issue](https://github.com/zenustech/zeno/issues) on GitHub, thanks for you support!


# Developer Build

To build ZENO, you need:

- GCC 9+ or MSVC 19+, CMake 3.12+, and Python 3.6+ to build ZENO.
- Pybind11, NumPy and PySide2 (Qt for Python) to run ZENO editor.
- (Optional) OpenVDB for building volume nodes; CUDA for GPU nodes.

> Hint: for Python, please try avoid using virtualenv and Conda if possible.
> WSL is also not recommended because of its limited GUI and OpenGL support.

Click links below for detailed setup for each platform:

- [Windows 10](/docs/dev_win10.md)
- [Ubuntu 20.04](/docs/dev_ubuntu20.md)
- [CentOS 7](/docs/dev_centos7.md)
- [Arch Linux](/docs/dev_archlinux.md)

After finishing building, use `run.py` to run ZENO for development! You may click `File -> Open` to play `graphs/LorenzParticleTrail.zsg` to confirm everything is working well :)


# Miscellaneous

## Write your own extension!

See [zenustech/zeno_addon_wizard](https://github.com/zenustech/zeno_addon_wizard) for an example on how to write custom nodes in ZENO.

----------------------------------------------------------------------------------------------------------

- **Legacy browser support (IE10+)**<br>
  Thoroughly tested and fully compatible with legacy browsers, including support for CSS custom properties (courtesy of a handy [ponyfill](https://github.com/jhildenbiddle/css-vars-ponyfill) developed specifically for docsify-themeable).

?> Like zeno? Be sure to check out [zeno-docs](https://github.com/zenustech/zeno-docs)!

## Contact & Support

- Create a [GitHub issue](https://github.com/jhildenbiddle/docsify-themeable/issues) for bug reports, feature requests, or questions
- Follow [@jiayaozhang](https://github.com/jiayaozhang) for announcements
- Add a ⭐️ [star on GitHub](https://github.com/zenustech/zeno) or ❤️ [tweet] to support the project!

## License

This project is licensed under the [Mozilla Public License](https://github.com/zenustech/zeno/blob/master/LICENSE).

Copyright (c) ZENUSTECH ([@ZENUS](https://github.com/zenustech/zeno))

<!-- GitHub Buttons -->
<script async defer src="https://buttons.github.io/buttons.js"></script>