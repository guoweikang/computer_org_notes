===============
Boolean Logic
===============

我们将讨论二进制的另外一种应用: 布尔表达
通过几种基础的微型电路，结合二级制的输入，可以组合成为复杂的控制电路


要求掌握
========
通过本章学习，应该能够掌握
 
 - 描述逻辑门的定义
 - 描述逻辑门的作用&实际应用 
 - 描述逻辑门的三种表达形式：电路、真值表、代数表达式
 - 分别描述三种基础逻辑门的电路、代数形式、真值表
 - 能够从 代数形式(电路) 推导出 电路(代数)、真值表 
 - 描述代数恒等式的作用
 - 证明布尔代数恒等式


逻辑门(Logic Gate)
===================



现实应用
---------
本节通过一个现实生活中很小的例子,来看一下boolean logic的应用 旨在更好的理解

.. note::

   我喜欢经常使用现实中的例子做类比或者参考，这样会更加生动并加深理解

让我们想像一下，野马轿车,如果你很熟悉汽车，你一定知道他最大的特色之一是他的车尾灯：

.. image:: ./images/2.png
  :width: 400px

我想说当他流水灯亮起来的时候 帅爆了，流水灯？你应该想到了 就是第一个灯亮 第二个、第三再亮 然后重复循环，OK 这样的软件/硬件怎么设计？

 + 一个定时器: 用来表示滴答
 + 一个2bits计数器：作为控制器，枚举不同的状态, 每次滴答，计数加1， 为什么是2bits？ 因为一共有四个状态: 灯1亮 灯12亮 灯123亮 灯123(灭) 
 
让我们用真值表来表示一下：假设A B是我们的2bit控制器 我们有三个输出(三个真值表) 输出分别控制 灯1 灯2 灯3，因为输入是一样的，我们把三个真值表合成一个:
 
+-----+------+------+-------+-------+
|  输入      |    输出              |
+=====+======+======+=======+=======+
|A    |  B   |  灯1 |   灯2 |  灯3  |
+-----+------+------+-------+-------+
|  0  |  0   |  0   |   0   |   0   |
+-----+------+------+-------+-------+
|  0  |  1   |  1   |   0   |   0   |
+-----+------+------+-------+-------+
|  1  |  0   |  1   |   1   |   0   |
+-----+------+------+-------+-------+
|  1  |  1   |  1   |   1   |   1   |
+-----+------+------+-------+-------+

让我们在看一下每个灯的控制逻辑(公式)：
 
 + 灯1亮(灭)的条件是：当AB输入任意1个是1亮，或者AB输入都为0的时候灭
 + 灯2亮(灭)的条件是：当A输入1亮，A输入0则灭
 + 灯3亮(灭)的条件是：当AB全部输入1亮，否则灭


逻辑门表达形式
--------------
上一小节我们通过一个现实场景，观察了逻辑门的应用，让我们在回头看看其中用到了哪些方法或者工具公式
 



XOR Gate
-----------


组合门
=======

我们已经学习了四种最基础的logic gate：Not，And, Or , Xor; 组合门我们暂且使用和逻辑门一样的定义：
有多个inputs，经过一个逻辑电路，输出1个output; 说是组合门，其实是指这个逻辑电路也是由基础的gate组成

从一个现实应用开始
------------------

接下来继续从一个实际场景入手

.. image:: ./images/8.png
  :width: 400px

如上图，我们假设有一间教室有： 
 
 - 窗户监视器: 坚实窗户是否遭到破坏 
 - 门探测器: 检测教室门是否被打开
 - 动作探测器：探测教室内部是否有物体移动
 - 报警系统： 根据教室的三个传感器输入，决定是否发出警报
 
最简单的报警条件: 
 如果窗户被破坏  OR  门被打开  OR  监测到人员移动，就发生告警，则电路图设计为下面即可 
 
.. image:: ./images/9.png
  :width: 400px

当上述三个探测器，任意一个发生感应 就进行告警，仅仅通过一个 OR GATE 完成 ；但是实际情况往往不是这样的;
在白天，老师和学生都会在教室里面走动，所以 motion 和 door detectors 总是会触发，这种情况下不应该有告警，
所以，我们可以通过在增加一个警报系统开关 

 - 系统开关：控制告警系统开启关闭， 白天关闭，晚上开启
 
更复杂的报警条件： 
 如果 （窗户被破坏 OR 门被打开 OR 监测到人员移动）AND （告警系统开启），就发生告警，则电路设计需要改为: 
 
.. image:: ./images/10.png
 :width: 400px

这里我们使用了之前学习过得基础门的数学表达式，还记得吗，A or B or C = A+B+C, (A+B+C) AND D =  (A+B+C)*D 
让我们在考虑一下更现实的情况，窗户被破坏，我们可能更加希望他一定会产生告警，而不需要受其他条件影响

更加复杂的报警条件：
 如果 窗户被破坏 OR ((门被打开 OR 监测到人员移动）AND （告警系统开启）)，就发生告警:
 
.. image:: ./images/11.png
 :width: 400px
 
接下来让我们尝试推导一下这个组合门的真值表,真值表推导也是从最基础的gate 依次推导

+-----+------+------+-------+-------+-------+------------+
|          输入             |        输出                |
+=====+======+======+=======+=======+=======+============+
|A    |  B   |  C   |  D    |   A+B |(A+B)*D| (A+B)*D + C| 
+-----+------+------+-------+-------+-------+------------+
|  0  |  0   |  0   |   0   |   0   |   0   |      0     |
+-----+------+------+-------+-------+-------+------------+
|  0  |  0   |  0   |   1   |   0   |   0   |      0     |
+-----+------+------+-------+-------+-------+------------+
|  0  |  0   |  1   |   0   |   0   |   0   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  0  |  0   |  1   |   1   |   0   |   0   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  0  |  1   |  0   |   0   |   1   |   0   |      0     |
+-----+------+------+-------+-------+-------+------------+
|  0  |  1   |  0   |   1   |   1   |   1   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  0  |  1   |  1   |   0   |   1   |   0   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  0  |  1   |  1   |   1   |   1   |   1   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  1  |  0   |  0   |   0   |   1   |   0   |      0     |
+-----+------+------+-------+-------+-------+------------+
|  1  |  0   |  0   |   1   |   1   |   1   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  1  |  0   |  1   |   0   |   1   |   0   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  1  |  0   |  1   |   1   |   1   |   1   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  1  |  1   |  0   |   0   |   1   |   0   |      0     |
+-----+------+------+-------+-------+-------+------------+
|  1  |  1   |  0   |   1   |   1   |   1   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  1  |  1   |  1   |   0   |   1   |   0   |      1     |
+-----+------+------+-------+-------+-------+------------+
|  1  |  1   |  1   |   1   |   1   |   1   |      1     |
+-----+------+------+-------+-------+-------+------------+


NAND Gate
----------

.. note::
 
  额外介绍一下低电平有效，我们已经知道逻辑门的输出都是一个个bool值，现实中由于电气电路原因，很多片选使能确往往不是我们想的：给一个高电平1 开启，低电平0 关闭 往往都是相反的，因为高电平更容易收到干扰(真实原因更多需要电气知识，小白一个，不深究了)


.. image:: ./images/12.png
 :width: 400px

上图是一个NAND GATE的电路图 我们观察到，Note gate 会以一种更加简便的方式隐含在电路图


布尔代数式
===========

我们已经学习了逻辑门的三种表达式： 电路图、代数式、真值表；电路、真值表都是相对固定的表达方式，代数式本身会存在数学特有的特点

我们也知道 可以通过代数式推导出其他两种形式,那么代数式能帮助我们解决什么问题，为什么我们要继续证明他








