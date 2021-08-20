# Introduction

[![CMake](https://github.com/zenustech/zeno/actions/workflows/cmake.yml/badge.svg)](https://github.com/zenustech/zeno/actions/workflows/cmake.yml) [![License](https://img.shields.io/badge/license-MPLv2-blue)](LICENSE) [![Version](https://img.shields.io/github/v/release/zenustech/zeno)](https://github.com/zenustech/zeno/releases)
<a class="github-button" href="https://github.com/zenustech/zeno" data-icon="octicon-star" data-show-count="true" aria-label="Star zenustech/zeno on GitHub">Star</a>

[Download](https://github.com/zenustech/zeno/releases) | [Repo](https://github.com/zenustech/zeno) | [About us](https://zenustech.com) | [Tutorial](https://zenustech.com/tutorial) | [Videos](https://space.bilibili.com/263032155) | [Q&A Forum](https://github.com/zenustech/zeno/discussions) | [Bug report](https://github.com/zenustech/zeno/issues)

[国内高速下载](https://gitee.com/zenustech/zeno/releases) | [Gitee 镜像仓库](https://gitee.com/zenustech/zeno) | [公司主页](https://zenustech.com) | [中文教程](https://zenustech.com/tutorial) | [视频教程](https://space.bilibili.com/263032155) | [问答论坛](https://github.com/zenustech/zeno/discussions) | [BUG 反馈](https://github.com/zenustech/zeno/issues)

Open-source node system framework, to change your algorithmic code into useful tools to create much more complicated simulations!

![rigid3.zsg](/images/rigid3.jpg "arts/rigid3.zsg")

ZENO is an OpenSource, Node based 3D system able to produce cinematic physics effects at High Efficiency, it was designed for large scale simulations and has been tested on complex setups.
Aside of its simulation Tools, ZENO provides necessary visualization nodes for users to import and run simulations if you feel that the current software you are using is too slow.

## Features

Integrated Toolbox, from volumetric geometry process tools (OpenVDB), to state-of-art, commercially robust, highly optimized physics solvers and visualization
nodes, and various VFX and simulation solutions based on our nodes (provided by .zsg file in `graphs/` folder).

## Gallery

![robot hit water](/images/crag_hit_water.gif)

![SuperSonic Flow](/images/shock.gif)


# Motivation

Nowadays, many CG artists have reached an agreement that creating arts (especially
physics simulation and animation) using visual-programming tool is very convinent and flexible.

This repo aims to provide a great tool for both technical artists and CG developers, and researchers from physics simulation.

## Easy Plug, Easy Go

One may create complicated simulation scenarios by simply connecting the nodes provided by the system. For example, here's a molecular simulation built by our users:

![lennardjones.zsg](/images/lennardjones.jpg "arts/lennardjones.zsg")

This is the charm of visual-programming, not only the direction of data-flow, but also the logic-flow of the solution algorithm is presented at no more clarity.
In fact, building this molecular simulation from scratch took no more than 7 minutes!

## Flexible

One can easily change or adjust a solution by simply break and reconnect of the nodes.
Unlike many simulation softwares that have fixed functionality, we provide the building
blocks of algorithms in the form of **nodes** at a relatively low granularity.
By connecting these nodes, you can literally create your unique solver that best fits
your need, rather than being limited by the imagination of software programmers.
For example, here @zhxx1987 created two-way coupled fluid-rigid simulation by adding some nodes to pass momentums from surfaces despite the FLIP solver didn't support fluid-rigid coupling at the first place:

![Rigid_pool2.zsg](/images/FSI.gif "arts/Rigid_pool2.zsg")


## Performant

ZENO nodes are mainly written in C++. By connecting nodes in our Qt5 editor,
you are invoking our highly optimized programs by our senior engineers. And
all you need to do is to explore in your mind-space without bothering to tackle 
low-level details.
Performance-wisely, it's shown by @zhxx1987 that our FLIP solver is 4x faster than
Houdini at large scale.

![FLIPSolver.zsg](/images/FLIPSolver.jpg "arts/FLIPSolver.zsg")

## Control-flows

Unlike many pure functional node systems (e.g. Blender), ZENO has a strong time-order
and provide a lot of control-flow nodes including CachedOnce, BeginForEach, EndFor, etc.
This enable you to make turing-equivalent programs that fit real-world problems.

![forloop.zsg](/images/forloop.jpg "arts/forloop.zsg")

## Simplicity

For those many outstanding systems with visual-programming abilities out there,
one may have a hard time integrate new things into those systems, often due to their
tight coupled design of data structures, as well as system archs. 
Zeno adopts a highly decoupled design of things, making extending it becoming super-simple.

Here's an example on how to add a ZENO node with its C++ API:

[![zeno_addon_wizard/YourProject/CustomNumber.cpp](/images/demo_project.png)](https://github.com/zenustech/zeno_addon_wizard/blob/main/YourProject/CustomNumber.cpp)

## Extensible

As a comparison, the ZENO node system is very extensible. Although ZENO itself
doesn't provide any solvers, instead it allows users to **write their own nodes**
using its C++ API.
Here's some of the node libraries that have been implemented by our developers:

- Z{f(x)} expression wrangler (by @archibate)
- basic primitive ops (by @archibate)
- basic OpenVDB ops (by @zhxx1987)
- OpenVDB FLIP fluids (by @zhxx1987 and @ureternalreward)
- Molocular Dynamics (by @victoriacity)
- GPU MPM with CUDA (by @littlemine)
- Bullet3 rigid solver (by @archibate and @zhxx1987)
- Hypersonic air solver (by @Eydcao @zhxx1987)
- MPM Mesher (by @zhxx1987)

Loading these libraries would add corresponding functional nodes into ZENO,
after which you can creating node graphs with them for simulation.
You may also add your own solver nodes to ZENO with this workflow if you'd like.

![demoproject.zsg](/images/demoprojgraph.jpg "arts/demoproject.zsg")

## Integratable

Not only you can play ZENO in our official Qt5 editor, but also we may install
ZENO as a **Blender addon**! With that, you can enjoy the flexibilty of ZENO
node system and all other powerful tools in Blender. See `Blender addon` section
for more information.

![blender.blend](/images/blender.jpg "assets/blender.blend")

<!--
## ZenCompute (@littlemine)

Open-source code development framework to easily develop high-performance physical simulation code that both run on cpu and gpu with out too much effort. Now intergrated into ZENO.

[![ZenCompute development framework](/images/zencompute.png)](https://github.com/zenustech/zpc)
-->


# Miscellaneous

## Blender addon

Blender user? Be sure to check out [ZenoBlend](https://github.com/zenustech/zenoblend)!

## Contact & Support

- Create a [GitHub issue](https://github.com/zenustech/zeno/issues) for bug reports, feature requests, or questions.
- Follow [@jiayaozhang](https://github.com/jiayaozhang) and [@archibate](https://github.com/archibate) for announcements.
- Add a ⭐️ [star on GitHub](https://github.com/zenustech/zeno) or ❤️ [tweet](https://twitter.com/archibate) to support the project!

## License

This project is licensed under the [Mozilla Public License 2.0](https://github.com/zenustech/zeno/blob/master/LICENSE).

Copyright (c) Zenus Technology ([@zenustech](https://github.com/zenustech))

<!-- GitHub Buttons -->
<!-- script async defer src="https://buttons.github.io/buttons.js"></script -->
