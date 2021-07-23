:github_url: https://github.com/jiayaozhang/ZenusTech-Documentation.git


开发者指南
======

开源的节点系统，我们只需要添加我们的算法就能加入更多更精彩的仿真啦！
-----------

.. image:: ../../_static/image/ZENO/rigid3.jpg


特性
^^^^^
我们的节点系统整合的工具箱从OpenVDB到各种商业软件，以及各个优化的物理求解器，不同的VFX。

各种仿真效果都可以基于我们的节点系统实现出来。具体参考（开源arts文件夹下面的.zsg 文件）

.. image:: ../../_static/image/ZENO/crag_hit_water.gif

.. image:: ../../_static/image/ZENO/saudi/shock.gif


ZENO高性能计算
^^^^^^^^^^^^^^^

ZENO现在已经可以轻松的同时在CPU和GPU上开发高性能物理仿真

.. image:: ../../_static/image/ZENO/zencompute.png


开发ZENO的原因
^^^^^^^^^^^^^

目前，很多图形学艺术家都希望能通过可视化编程能高效快捷的开发出物理仿真和动画。

ZENO的目的就是通过节点仿真为图形开发者和艺术从业者提供极大的便利

一个很复杂的物理仿真可以通过简单的节点连接就能实现
这也是可视化物理仿真的魅力所在。七分钟不到就可以将逻辑与数据流清晰的可视化出来

.. image:: ../../_static/image/ZENO/lennardjones.jpg

柔韧性
^^^^^^^^^^^^^^^
ZENO节点可以轻松的改变和调整结果，通过轻松的删除连线并重新连上节点。不像传统的仿真软件，有固定的功能，我们将算法堆积成了积木，并通过连接这些节点我们就可以创造出我们自己的解算器。而不会由于软件而限制了开发。

.. image:: ../../_static/image/ZENO/FSI.gif

性能
-------------

ZENO节点主要是由c++来写的。通过Qt5编译器来连接节点，这些节点由我们开发人员来做就好了，你所需要做的就只是脑洞大开。如下图所示，心欣做的FLIP Solver就比houdini的四倍还快

.. image:: ../../_static/image/ZENO/FLIPSolver.jpg

控制流
^^^^^^^^^^^^^^^^^^^^^^^^
不像传统的节点系统（Blender)，ZENO有着很强的时间序列并提供了很多控制流节点包括CachedOnce, BeginForEach, EndFor等。这些就能帮你微调来适应真实的问题。

.. image:: ../../_static/image/ZENO/forloop.jpg


统一性
^^^^^^^^^^^^
尽管如今我们已经有很多节点系统了，但是他们都限制在一些特定的软件里面，比如Blender，Houdini, Unreal等等。
这些软件有很多节点和前提限制，导致开发人员很难拓展开。比如，一个在Blender做布料模拟的人很难在同时在houdini做流体仿真。这也是我们开发ZENO的主要目的。

.. image:: ../../_static/image/ZENO/demo_project.png

可拓展性接口
-------------

1. basic primitive ops (by @archibate)
2. basic OpenVDB ops (by @zhxx1987)
3. OpenVDB FLIP fluids (by @zhxx1987 and @ureternalreward)
4. Tree-code N-body (by @archibate)
5. Molocular Dynamics (by @victoriacity)
6. GPU MPM with CUDA (by @littlemine)
7. Bullet3 rigid solver (by @archibate)
8. Hypersonic air solver (by @Eydcao)

载入这些库可以将一系列的节点载入到zeno,同时你也可以在ZENO中加入自己的solver

.. image:: ../../_static/image/ZENO/demoprojgraph.jpg


整合性
-------------

与此同时，我们也把ZENO加入到了Blender插件里面，这样你就可以自由的发挥ZENO节点系统来画出你想要的物理仿真啦

.. image:: ../../_static/image/ZENO/blender.jpg


用户终端安装
^^^^^^^^^^^^


下载
-------------
Go to the release page, and click Assets -> download zeno-linux-20xx.x.x.tar.gz. Then, extract this archive, and simply run ./start.sh, then the node editor window will shows up if everything is working well.


使用
---------------
There are some example graphs in the ./arts/ folder, you may open them in the editor and have fun! Currently rigid3.zsg, FLIPSolver.zsg, prim.zsg, and lennardjones.zsg are confirmed to be functional. Hint: To run an animation for 100 frames, change the 1 on the top-left of node editor to 100, then click Execute. Also MMB to drag in the node editor, LMB click on sockets to create connections. MMB drag in the viewport to orbit camera, Shift+MMB to pan camera.

Bug 报告
-------------------
If you find the binary version didn't worked properly or some error message has been thrown on your machine, please let me know by opening an issue on GitHub, thanks for you support!



开发者使用指南
^^^^^^^^^^^^^^^

安装需求
----------

You need a C++17 compiler, CMake 3.12+, and Python 3.6+ to build ZENO; NumPy and PyQt5 to run ZENO editor. Other requirements like Pybind11 or GLAD are self-contained and you don't have to worry installing them manually.

Arch Linux
-----------
sudo pacman -S gcc make cmake python python-pip python-numpy python-pyqt5 qt5-base libglvnd mesa


Ubuntu 20.04
--------------
sudo apt-get install gcc make cmake python-is-python3 python-dev-is-python3 python3-pip libqt5core5a qt5dxcb-plugin libglvnd-dev libglapi-mesa libosmesa6

python --version  # make sure Python version >= 3.7
sudo python -m pip install -U pip
sudo python -m pip install numpy PyQt5


Windows 10
--------------
1. Install Python 3.8 64-bit. IMPORTANT: make sure you Add Python 3.8 to PATH! After that rebooting your computer would be the best.
2. Start CMD in Administrator mode and type these commands:

python -m pip install numpy PyQt5


(Fun fact: you will be redirected to Microsoft Store if python is not added to PATH properly :) Make sure it starts to downloading and installing successfully without ERROR (warnings are OK though).

If you got ERROR: Could not install packages due to an EnvironmentError: [Errno 13] Permission denied: 'c:\\python38\\Lib\\site-packages\\PyQt5\\Qt5\\bin\\d3dcompiler_47.dll'': Quit anti-virus softwares (e.g. 360), they probably prevent pip from copying DLL files.

If you got ImportError: DLL load failed while importing QtGui: Try install Microsoft Visual C++ Redistributable.

3. Install Visual Studio 2019 Community Edition or later version (for C++17 support in MSVC).


