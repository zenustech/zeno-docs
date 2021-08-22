# ZENO中的各种子功能

## 可视化功能

在ZENO中， 我们内置了一些可视化节点帮助用户对仿真数据进行可视化， 结合ZFX以及对Heatmap的调整， 设计简单的可视化节点实则妙用无穷， 在此，我们介绍两种常见的使用场景：

1. 对于标量场的显示
显示标量场可以借由ZENO的VDBSlice节点实现， 这是一个官方节点， 可以通过`File->import->OfficialSubnets/vdbslice..zsg`来导入到系统中使用(自动化导入会在下一个小版本完成更新)

![example](/images/Visual/1.png)

加载后, 该节点会出现在右键`->visualize->VdbSlice`, 或者也可以通过tab->输入VdbSlice快速搜索再回车来完成.

将该节点添加到节点编辑面板,它长这样:

![example](/images/Visual/2.png)

这个节点对应接收一个vdb网格, 并通过提供的channelName床创建一个携带”channelName”的, 分辨率为resolution的Primitive网格, 该网格的中心会被放置在origin位置, 转向normal方向, 并采样将”channelName”采样VDB数据后输出

![example](/images/Visual/3.png)

之后, 我们再把采样出来的primitive交给我们的热力云图着色工具进行着色, 这个可视化的对象是一个从三维模型文件中计算得到的SDF(符号距离场), 黑色在里, 白色在外, 红色接近isosurface=0处. VdbSilic节点支持从任何角度切割一个体积场, 得到有效的可视化数据.

## 对于矢量场的显示

在ZENO中显示矢量场, 则需要使用VolumeTrail节点. 通过`File->import->officialSubnets->volumeTrail`来导入volumeTrail节点有关的组件,VolumeTrail节点接受一个矢量场数据并对其进行矢量方向追踪, 一个典型的结果如下图所示:

![example](/images/Visual/4.png)

该节点会沿着输入速度场追踪路径线, 并自动地按照热力云图对速度的大小进行可视化

![example](/images/Visual/volume.gif)

![example](/images/Visual/zfx.gif)

## AlgoLink功能

在这一个教程中，我们向大家介绍一下zeno强大的AlgoLink功能以及如何基于zeno的AlgoLink功能创建可被复用的ZENO subnets。

ZENO最大的优势就是可以使用其强大的连接功能将不同的算法节点组合起来产生无穷的变化。
比如可以通过使用zeno的节点相连接， 组合成功能更强大的subnet， 一个subnet的编辑包括了以下几个重要概念：

![example](/images/AlgoLinkTools/1.png)

Category： 决定了它将会被系统归类到哪一个category
Input， ouput， 定义了这个subgraph被使用时的输入和输出接口，数据将可以通过subgraph的输入接口进入系统，被计算使用后， 从输出接口传送到之后的计算节点。 
一个subgraph中的算法可以自由定义，就和编程中开发函数一样， 一旦定义完成后，整个subgraph就等价于是一个节点执行单元，可以被主进程调用。

![example](/images/AlgoLinkTools/2.png)

一个subgraph被开发完后看起来是这样的：

![example](/images/AlgoLinkTools/3.png)

其中被勾选了VIEW的节点， 等价于整个subgraph的被可视化对象

![example](/images/AlgoLinkTools/4.png)

该对象， 当且仅当该subgraph在被主进程调用时被勾选了可视化，就会被可视化窗口进行可视化输出， 如下图所示

## Z{f(x)}功能

Z{f(x)}是zeno使用的脚本语言，该脚本语言语法简便，可用于描述一个简单的数学公式，一经实现，可并行地运行在CPU或者GPU设备上，是场景编辑的强大工具。

它支持用户编辑一段数学公式, 并行地对几何或者仿真数据进行计算编辑, 一个zfx脚本以及一个参数列表我们称之为 Wrangler, 用于接收Wrangler和并行处理仿真数据的节点则是Wrangle.(该叫法来自于Houdini). 我们对物理仿真计算做了抽象Wrangle, 目前来看, 足以支持从分子动力学仿真, 到SPH仿真, 到粒子-网格仿真, 到天体力学仿真的所有物理计算模式。

![example](/images/Z{f(x)}/1.jpg)
![example](/images/Z{f(x)}/zh1.jpg)

值得一提的是, zfx结合wrangle是可以无差别地并行运行在CPU以及GPU上的, 在我们的测试中, wrangle(GPU模式)比wrangle(CPU模式)有100倍的加速比. Z{f(x)}的运行无需编译, 无需编译, 无需编译. 这大大加速了仿真设计者(TD)对于场景的开发自由度.

比如以下这个场景
![example](/images/Z{f(x)}/6.png)

一个类似于海滩的设置, 用来研究海浪在海滩边卷起的样子和能量. 在这个场景中, 如何产生海浪的边界条件是个问题, 我们参考现实中 wave pool(海浪池)的机械原理, 用zfx制作了我们的海浪产生装置

![example](/images/Z{f(x)}/wavgen.gif)

总结

造浪器优于海浪边界速度方程在于它不会向水体中emit新的水也不用设置过于复杂的出口条件, 基于物理实际环境, 只要把造浪器的机械运动规律调整正确, 基本上就可以获得足够真实的海浪运动.Z{f(x)}作为一个zeno的新特性, 具有并行化, GPU/CPU无差别运行等优势, 且无需编译, 可以快速地提供给创作者用以对场景进行编辑和调整, 快速得到反馈, 产生更多样的变化和结果. 在这个场景中很快地编辑出了造浪器的运动模型. 以上场景仿真耗时约2小时. 每帧约5000万粒子. 以1/24秒为frame单位, 共仿真300frame, 播放120~288.

![example](/images/Z{f(x)}/wave.gif)

一个简单的ZFX使用场景如下所示：

![example](/images/Z{f(x)}/1.png)

在这个场景中每个frame， zfx所表达的运算会被并行地施加给prim端口连入的几何图形，该根据ZFX所述， 该物体的pos会从它最初的位置被沿着法线方向往复反转， 其中time是我们从参数列表中获取进来的系统级变量， 它由GetTime函数来得到。 这个案例的运行结果如下所示：

![example](/images/Z{f(x)}/zfx.gif)

@符号表示这个变量属于被修改的primitive, 或者原primitive没有, 会被添加上去. $的意思是这是一个dict传递进入的变量. 此外@pos @nrm @clr @vel @rad等关键字, 是保留关键字, 是zeno系统对于坐标， 法线， 速度， 粒子半径的一般假设 事实上, 从简单的几何与图元操作, 到更复杂的物理仿真(比如NBody星体仿真, 都可以直接由ZFX开发完成)

![example](/images/Z{f(x)}/colorfulZello.gif)

![example](/images/Z{f(x)}/wave.gif)

![example](/images/Z{f(x)}/points.gif)

![example](/images/Z{f(x)}/NBodyCode.png)

![example](/images/Z{f(x)}/6.gif)
## 流体模拟功能

### ZENO上快速实现拉格朗日流体模拟功能
这篇文章将介绍如何使用zeno快速实现拉格朗日流体模拟。通过简单的连连看编程，即可实现场景布置、可视化效果；通过解释性语言zfx，无需编译，即可快速实现拉格朗日流体模拟。

### 背景介绍

1. ZENO

ZENO,是我司倾力打造出来的可视化“编程”工具。使用ZENO，可以极大程度上帮助我们从繁重的代码工作中解放出来。通过“连连看”的编程方式，即可快速搭建场景、构建模型以及实现模型的可视化。

2. ZFX

ZFX是ZENO自主开发的解释过程。ZFX设法把计算映射到预先编译好的函数指针的内存段中，这些函数在安装ZENO时即已编译完毕，后续用户使用无需再次编译，just in time!

3. 流体模拟

在流体的模拟中，主要分为拉格朗日视角下的流体模拟与欧拉视角下的流体模拟两类。从数学的角度看，欧拉视角下的流体模拟是对流体求解偏导运算；而拉格朗日视角下的流体，是对流体求解进行全导运算。

本文介绍了拉格朗日流体的模拟。在模拟中，我们采用了Smoothed Particle Hydrodynamics(SPH)技术。该技术将流体离散化为一个个带有质量的流体粒子，并通过与周围粒子进行插值操作计算流体域中的量。篇幅有限，本项目所涉及到的理论与算法，请查阅参考文献。

后面我们一步一步的来介绍，如何使用ZENO做出流体模拟的效果出来。

### 搭建场景
首先，我们需要搭建一个场景，为此我们创建了子图GenParticles。

我们可以使用ZENO自带的简单的节点MakeCubePrimitive生成一个立方体形状的流体。 这里我们以碗为例，构造碗的方式如下：

![example](/images/fluidsimulation/exp2.jpg)

我们将这两个粒子模型合并在一起，作为该子图的输出：

![example](/images/fluidsimulation/exp3.jpg)

这样我们的场景即可搭建完毕。

![example](/images/fluidsimulation/exp4.jpg)

搭建准备
为了搭建一个隐式不可压缩SPH流体模型，我们首先对我们的粒子做好准备工作。为此，我们新建了子图initSPH。

![example](/images/fluidsimulation/exp5.jpg)
在这个子图里我们首先添加了粒子所需要的属性。随后计算每个粒子的标准体积：

![example](/images/fluidsimulation/exp6.jpg)
这个粒子准备步骤，整个仿真过程只需要执行一次，因此打上一个once标记

![example](/images/fluidsimulation/exp7.jpg)

后面就进入到了每个时间步的循环迭代中。

搭建构建
在每个时间步，我们需要去求解流体运算的Navier-Stokes方程。在这个过程里，最花费时间的是使得流体不可压缩的压强力的计算。该项目目前考虑了流体的粘性、重力以及压强力，我们采用分步积分的方式，先去求解流体的粘性与重力，随后放入压强的泊松方程中去计算压强力。为此，我们在子图SPHstep里作如下设计：

![example](/images/fluidsimulation/exp8.jpg)

第一个节点计算了求解压强的泊松方程里的常数项，包括当前粒子的体积、速度的散度等。第二个节点进入了Jacobi迭代求解压强的过程。第三个节点对粒子所受到的压强力做对流积分。这三个节点内部均由ZENO节点与ZFX实现。

以computePress节点为例证明我们系统构建的方便性。下图是Jacobi迭代的控制流程：

![example](/images/fluidsimulation/exp9.jpg)

将BeginFor与EndFor节点的FOR接口连起来做配对，DST与SRC端口之间的节点即循环所执行的代码。

循环的第一步，我们先计算压强加速度，这通过如下方式计算：


![example](/images/fluidsimulation/exp10.jpg)

其中hashGrid通过ZENO提供的ParticlesBuildHashGrid节点实现。该节点将流体粒子离散化到三维网格中。

![example](/images/fluidsimulation/exp11.jpg)

而在ParticlesNeighborWrangle节点内部，通过hashGrid查询粒子的邻域网格，实现近邻粒子的快速查询。而zfxCode端口则接入我们希望执行的zfx代码。由于zfx的特殊设计，写完即可立即执行无需编译，简直不能更爽，这一点相信写过大型程序的同学们肯定深有体会。

照猫画虎的，将算法的整个流程在ZENO上实现完成，即可看到最终的效果：


![example](/images/fluidsimulation/sph.gif)

模块化使用
我们将模型封装成子图后，后续如果我们还需要使用时，仅需要调用这三个节点，输入对应的参数即可快速搭建SPH流体模拟器，集成度非常高。

![example](/images/fluidsimulation/exp12.jpg)

编程调试
ZENO提供了很方便的调试工具。在这个可视化编程工具里，我们不仅可以避免等待编译的痛苦，还可以通过heatmap来查看每个粒子的状态。如下图所示，我们使用蓝色来对粒子进行着色，颜色越深则速度越小。可以看到，边界处的流体速度较快，而中心区域的流体速度小，这给了我们一个很直观的效果。

![example](/images/fluidsimulation/exp13.jpg)

同时，还可以通过调节粒子的半径，来判断该粒子当前的体积大小。可以看到，外围的粒子因为邻域粒子少，体积较大；碗内部的粒子密集，所以体积较小。

![example](/images/fluidsimulation/exp14.jpg)

参考文献
* [1]. Müller M, Charypar D, Gross M H. Particle-based fluid simulation for interactive applications[C]//Symposium on Computer animation. 2003: 154-159.

* [2]. Band S, Gissler C, Ihmsen M, et al. Pressure boundaries for implicit incompressible SPH[J]. ACM Transactions on Graphics (TOG), 2018, 37(2): 1-11.