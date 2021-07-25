:github_url: https://github.com/jiayaozhang/ZenusTech-Documentation.git


ZENO中的AlgoLink功能
=====================

在这一个教程中，我们向大家介绍一下zeno强大的AlgoLink功能以及如何基于zeno的AlgoLink功能创建可被复用的ZENO subnets。

ZENO最大的优势就是可以使用其强大的连接功能将不同的算法节点组合起来产生无穷的变化。
比如可以通过使用zeno的节点相连接， 组合成功能更强大的subnet， 一个subnet的编辑包括了以下几个重要概念：

.. image:: ../../_static/image/AlgoLinkTools/1.png

Category： 决定了它将会被系统归类到哪一个category
Input， ouput， 定义了这个subgraph被使用时的输入和输出接口，数据将可以通过subgraph的输入接口进入系统，被计算使用后， 从输出接口传送到之后的计算节点。 
一个subgraph中的算法可以自由定义，就和编程中开发函数一样， 一旦定义完成后，整个subgraph就等价于是一个节点执行单元，可以被主进程调用。

.. image:: ../../_static/image/AlgoLinkTools/subnet.gif

一个subgraph被开发完后看起来是这样的：

.. image:: ../../_static/image/AlgoLinkTools/2.png

其中被勾选了VIEW的节点， 等价于整个subgraph的被可视化对象

.. image:: ../../_static/image/AlgoLinkTools/3.png

该对象， 当且仅当该subgraph在被主进程调用时被勾选了可视化，就会被可视化窗口进行可视化输出， 如下图所示

.. image:: ../../_static/image/AlgoLinkTools/4.png
