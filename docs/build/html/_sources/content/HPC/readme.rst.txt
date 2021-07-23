:github_url: https://github.com/jiayaozhang/ZenusTech-Documentation.git


开发者指南
======

开源的节点系统，只需要给出你们的idea，就能用ZENO实现出更多更精彩的仿真啦！
-----------

.. image:: ../../_static/image/ZENO/rigid3.jpg


特性
^^^^^
我们的节点系统整合的工具箱从OpenVDB到各种商业软件，以及各个优化的物理求解器，不同的VFX。

各种仿真效果都可以基于我们的节点系统实现出来。具体参考（开源arts文件夹下面的.zsg 文件）

.. image:: ../../_static/image/ZENO/crag_hit_water.gif

.. image:: ../../_static/image/ZENO/shock.gif


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
点击到 release page, 然后勾选 Assets -> download zeno-linux-20xx.x.x.tar.gz. 解压zip文件, 然后 run ./start.sh, 然后节点系统的编译器就会自动显示出来


使用
---------------
在arts文件夹下面有一些样例图，你可以在编译器将他们打开然后设计出自己的物理仿真模型。 目前rigid3.zsg, FLIPSolver.zsg, prim.zsg, 和 lennardjones.zsg还在完善中
提示：如果想要运行一个100帧的动画，可以右上角的1改成100，并点击execute。


Bug 报告
-------------------
如果你发现binary版本不对或者不匹配，欢迎在ZENO下面提issue


开发者使用指南
^^^^^^^^^^^^^^^

安装需求
----------

你需要有 C++17 compiler, CMake 3.12+, and Python 3.6+ 来构建 ZENO; NumPy and PyQt5 运行ZENO的编辑器. Pybind11 或者 GLAD 是内置的，所以你不必担心是否需要自己安装

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
1. Install Python 3.8 64-bit. 重要: 确保你把python 3.8加入到路径里面! 重启后效果更佳！
2. 在命令行敲CMD并输入以下命令:

python -m pip install numpy PyQt5

（搞笑的事实：你会被指向Microsoft store如果python的路径没有安装正确的话 ：） 所以确保下载和安装成功，没有error，一般的warnings是ok的）

出现这种错误时: Could not install packages due to an EnvironmentError: 
[Errno 13] Permission denied: 'c:\\python38\\Lib\\site-packages\\PyQt5\\Qt5\\bin\\d3dcompiler_47.dll'': 
尝试退出一些杀毒软件比如说：360杀毒软件, 因为他们可能会阻止 pip 复制 DLL files.


如果你有导入错误： 当输入QtGui的时候，DLL输入失败：尝试安装 Microsoft Visual C++ Redistributable。


1. 安装 Visual Studio 2019 社区版或者更后的版本 ( C++17 支持的).


