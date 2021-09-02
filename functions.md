# ZENO中的各种高级功能


## 初识ZENO节点，与ZFX并行脚本语言

[![IMAGE_ALT](/images/t1.png)](https://www.bilibili.com/video/BV1tq4y1Q7cj?spm_id_from=333.999.0.0)

首先右键菜单选择 primitive里面的Make3DGridPrimitive节点，其中的nx是需要输入input的，这里我们点 shift+a，输入numericInt并与nx连起来

![example](/images/zfx1.png)

接下来把Make3DGridPrimitive节点上的VIEW点亮，在点击Run，就能看到Display上面能显示出对应的mesh了. 接下来我们还可以再加一个zenofx节点里面的ParticlesWrangle功能

![example](/images/zfx2.png)

在这里面，@clr=@pos,代表了颜色会随着position的变化而改变， @rad=length(@pos)代表着球的半径会随着球的position而改变

![example](/images/zfx3.png)

同时我们还可以添加NumericFloat节点和MakeDict节点，表示扩大原来的mesh到十倍

![example](/images/zfx4.png)

同时GetFrameNum节点和GetFrameTime节点可以帮我们得到当前的帧数和每一帧的时间. 总而言之就是有了zfx以后， 我们就可以在zeno里面控制非常高的自由度了

![example](/images/zfx5.png)

当然除了粒子以外，我们还可以导入三角网格。如图就是从asset文件夹里面导入猪头三角网格


## 详解Numeric和Primitive节点，并用他们制作动画

[![IMAGE_ALT](/images/t2.png)](https://www.bilibili.com/video/BV1Lf4y1G79W?spm_id_from=333.999.0.0)

NumericFloat节点用于得出float的值，PrintNumeric节点用于在显示出节点的值

![example](/images/num1.png)

此外zeno也支持NumericVec3来做矢量分析计算，在NumericOperator里面可以做sin, cos, atan 还有其他运算，lhs表示只做一元运算，rhs表示二元运算

![example](/images/num2.png)

这里面在点击一下view，就可以看到平滑的猪头脸了

![example](/images/num3.png)

也可以在zeno里面加PrimitiveSplitEdges这样的话，就可以看到棱角分明的mesh了. PrimitiveSplitEdges节点里面的mute可以使得生成的mesh变得很平滑

在TransformPrimitive里面将translation和NumericVec3节点相连就可以上下左右移动了。同时，eulerXYZ和NumericVec3节点相连，就可以在三维坐标里面任意旋转。

![example](/images/num4.png)

如图所示，NumericOperator里面lhs可添加NumericCounter用于计算帧数，NumericVec3用户作为mesh的旋转方向. 这也是节点编程实现动画的一个典型例子

ExportPrimitive节点可以用来导出节点

![example](/images/num5.png)

还可以在blender里面下载stop-obj.zip插件然后从preference里面导入其插件, 从而可以导出任何一帧的obj或者obj animation

## 使用OpenVDB节点进行SDF操作（膨胀、腐蚀、顶帽、黑帽）



## 自制几何节点插件，妙用SDF实现猴头沾水动画




## 开源流体仿真插件，更逼真的液体表面




## 开源流体仿真插件，创建液体流入点