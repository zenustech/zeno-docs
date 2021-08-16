:github_url: https://github.com/jiayaozhang/ZenusTech-Documentation.git


Primitive 三角网格
================================

Primitive表示一堆粒子，每个顶点都有其自己的属性，pos属性表示位置，vel属性表示速度，clr表示颜色，rad表示半径，nrm表示三角形网格顶点点的法线

下图表示从左往右分别表示将三角网格导出，导入。

.. image:: ../../_static/image/install_guide/exportprimitive.png

此外，我们还可以将obj文件制作成2D，3D以及cube类型的三角网格

.. image:: ../../_static/image/install_guide/makeprimitive.png

Primitive文件也可以转化成mesh, particles, tracetail，或者通过transformprimitive的格式来转变形

.. image:: ../../_static/image/install_guide/primitive2mesh.png

还可以将Primitive制作成lines， simple points, simple quads和simple Tris.

.. image:: ../../_static/image/install_guide/primitiveline.png

不同的mesh之间，也可以下图中的merge，mix， resize等进行操作从而得到我们自己想要的model

.. image:: ../../_static/image/install_guide/primitivemerge.png

