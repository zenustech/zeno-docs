:github_url: https://github.com/guochengqian/KAUSTian_Handbook_CN


Example 4 在Zeno中执行一个For循环
=======

4.1 for循环
-------

.. image:: ../../_static/image/Examples/4_for_1.jpg

Zeno中的for循环有几个重要组成部分: count(执行次数)FOR接口的连接(BeginFor->EndFor对), 以及由DST出发经过系列计算操作到达EndFor的 SRC的通路. 这条通路上的计算结点将会被执行count次.


4.2 for Each循环
--------

.. image:: ../../_static/image/Examples/4_for_2.jpg


当我们有一个物体列表时(列表由zeno的AppendList节点创建), 我们也可以使用ForEach循环, 它会自动给出当前循环的Object以及index值, 并可以运用这两个数据对物体进行操作. 上图中, 我们获取ObjectList中的物件, 随后, 根据index%7获取彩虹颜色列表中的颜色给物体指定颜色.



4.3 Break For 循环
---------

.. image:: ../../_static/image/Examples/4_for_3.jpg


当index大于5的时候终止执行


