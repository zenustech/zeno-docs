# Examples

## Example 1 Hello World

ZENO几个重要概念：
1. 内置的几何数据结构
2. 可视化编程系统
3. 高性能计算框架
4. 软件以及官方用代码或者zeno的可视化编程本身开发的工具

![hw](/images/Examples/helloworld.jpg)

在这个例子中， 我们演示了一个zelloWorld的简单案例， 这个案例有三个部分构成：用户提供一个字符串-->通过zelloWorld节点根据字符串产生3D字图形（只有大写）-->使用闪烁渲染进行可视化。同时，这也是一个典型的zeno界面， 它总共有这几个部分组成：一个三维观察窗口， 用于观察ZENO系统中的三维物体， 底下是一些frame调整功能， 再之下是节点编辑窗口， 这三者构成了ZENO的主要概念：对于时间轴的可视化编程。

## Example 2 Tag和连线,关键词

![hw1](/images/Examples/2_3D_1.jpg)

Zeno中的节点有以下几个重要的编辑概念

### Control Tag
这些tag浮动于节点上方，被开启后会显示为绿色


### Out
当该Tag被点亮时，由ZENO节点图所定义的程序逻辑， 无论多么复杂， 到达该节点的通路上的前置计算节点（以及通路上所需要的数据和数据所需的前置计算结点）会被必然依序执行（每个frame）， 直到最后一个out节点为止。节点的执行顺序由zeno系统保证：任何一个被需要的节点必然在任何需要其的节点之前被执行。

### Mute
当该Tag被点亮时，相应的节点会被取消执行， 注意，这也许会在整个图中引入错误， 比如被跳过的节点正好将一个数据类型A转换为后续计算所需要的数据类型B时。谨慎使用

### Once
当该Tag被点亮时， 所标记的节点只会在全局被执行一次。ZENO系统的最基本计算单位为substep（subframe）， 所有位于节点编辑器中的计算， 都会默认地被每个frame的每个subframe执行，然而很显然我们不是总需要这么做：比如读取一些与时间无关的静态的场景文件时，读取操作只需要执行一次。 对于这样的目的， 我们可以指定ONCE


### View
被打了VIEW的节点， 其计算结果， 当是renderable的物体时，会进入到zeno的3D可视化窗口被可视化， 可视化的方法由zeno的可视化节点决定。被标记VIEW的节点， 其所有前置计算也会被正确执行。当一个frame存在多个subframe， 以及当一个被标记数据可能在计算顺序中被先后修改时，只有最后一个subframe的最后一次修改结果才会进入可视化界面进行可视化

### 数据端口连线

![rexample](/images/Examples/3_Tag_2.jpg)


除了特殊端口，SRC，COND，DST以外的端口即数据端口，当一个右侧的数据端口被连向一个左侧的数据端口时，两个节点即构成了计算依赖关系， 前序节点会优先于后续节点被执行， 后续节点的数据输入为所对应连接的数据出口。

* 特殊端口：DST， SRC除了数据依赖关系外， 可以通过DST和SRC连接来强制指定计算执行顺序， 考虑如下计算图：

![rexample](/images/Examples/3_Tag_3.jpg)


在该流程所代表的计算图中， 我们企图对于读取的图形做CSG相减操作

图形---->上路:对它的所有坐标乘以0.5(inplace修改)-->转换为SDF, 给予VDB combine A. ----> 下路: 转换为SDF, 给予VDB Combine B然而结果, 我们没有得到任何输出图形, 原因是上路的图形的操作是inplace的, 而这两个岔路的执行顺序是按照创建顺序, 当上路的primitive 被inplace修改结束后, 下路的primitive数据(同一个指针位置)也被修改了, 于是乎我们实际上是在对数值相同的Primitive进行SDF转换和CSG操作, 当然没有结果.

![rexample](/images/Examples/3_Tag_4.jpg)

当出现对于数据的In-Place操作可能会修改其它分支链路的计算结果时, 我们可以通过DST->SRC强制修改节点执行的顺序, 如此, 原先的Primitive会被先转化为一个SDF, 再被进行缩放修改, 转化为另一个SDF, 如此,我们就会对两个数值不同的SDF进行CSG操作, 从而得到正确的结果

![rexample](/images/Examples/3_Tag_5.jpg)

zeno中提供了一些重要的节点对于系统级的变量(比如frame, time等的)进行设置和获取, 以支持用户在计算中出于不同的目的对于系统变量和状态进行控制和利用. 比如

![rexample](/images/Examples/3_Tag_6.jpg)

这将会在一个frame的subframe中对物体的形态按照系统变量framePortion(当前frame时间积分完成的百分比)进行插值, 提供更精细化的边界或者运动控制

![rexample](/images/Examples/3_Tag_7.jpg)

而{frame}字符将把目标数据在当前frame结束时自动命名为正确的序号名称并保存到硬盘上.

以上构成了zeno最基本的一些计算和操作概念, 我们将在之后的章节中通过更多的案例和练习深化这些概念, 带领大家往zeno的深水区进发

## Example 3 读取并显示三维文件

![robot hit water](/images/Examples/2_3D_1.jpg)

在zeno中可以读取并显示三维物体(这个功能还在进步中, 会做成自动对输入多态和输出多态的支持)比如读取一个mesh,并显示(上图)

或者:读取一个VDB 数据将SDF转换为polygon并显示(下图):

![robot hit water](/images/Examples/2_3D_2.jpg)


## Example 4 执行For循环

### For循环

![example](/images/Examples/4_for_1.jpg)

### For Each 循环

![example](/images/Examples/4_for_2.jpg)

### Break For循环

![example](/images/Examples/4_for_3.jpg)

## Example 5 条件控制

![example](/images/Examples/5_1.jpg)

![example](/images/Examples/5_2.jpg)

如果frame是奇数, 读取sphere.obj并显示, 如果frame是偶数, 读取monkey.obj并显示. IFElse节点会根据输入条件在两条分支道路中选择一条执行并把对应路径的执行结果传递给result出口. 共后续节点使用.

## Example 6 封装子图并被调用

Zeno中最强大的功能之一就是用zeno封装子图并被zeno的其它场景作为一个节点调用. 由此可以两仪生四象 , 四象生八卦, 变化无穷.

下图:一个mesh和它被ReCenter(减去质心)后的位置

![example](/images/Examples/6_1.jpg)


开发一个subnet(子图)节点就如同开发一个函数, 可以自定义它的输入和输出, 以及它可能被可视化捕捉的对象, 在以下这个最简单的实现中, 我们展示了这样一个逻辑: 首先对于输入的图元, 我们对它进行ParallelReduce操作求其坐标”pos”的均值, 这就是它的几何质心(这基于它的每个三角形都差不多大, 如若不然我们可以使用remesh对它先做remesh). 然后, 我们将图元的每一个pos都减去这个均值, 就得到它被recenter后的坐标了. 我们再输出com以及prim, 以供后续节点使用


![example](/images/Examples/6_2.jpg)


这样一个节点被封装完毕后, 它就和任何一个由cpp开发出来的节点一样可以被调用, 并且还可用于其它的子图中, 甚至自己调用自己(递归). 事实上, zeno的很多官方算法甚至都是由subnet开发的, 而非cpp开发.

未完待续…..

Example 7 在ZENO中编辑一个公式(zfx)

Example 8 在zeno中进行刚体仿真

Example 9 VDB以及体积操作的妙用

Example 10 在zeno中进行刚体仿真

Example 11 在zeno中进行流体仿真

Example 12 在zeno中进行MPM仿真

Example 13 在zeno中进行气体仿真

Example 14 在zeno中进行肌肉仿真

Example 15 在zeno中进行分子动力学仿真

Example 16 zeno的Wrangler

Example 17 用C++扩展zeno:如何用编程开发一个节点?

Example 18 用zeno扩展zeno, 以实现一个SPH解算系统为例

Example 19 ZENO与纯CPP开发出的并行程序的性能对比

Example 20 ZENO与直接开发cuda代码程序的性能对比

Example 21 场景实战: 狂风, 海中方舟, 镇龙塔倒, 龙腾出海.

Example 22 场景实战: 程序化生成场景