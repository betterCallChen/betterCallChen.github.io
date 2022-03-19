---
layout: page
title: 
permalink: /imaging/active_illumination_model
---

***<font size=6>关于active illumination based sensing的简单模型</font>***

一般情况下，如果光线充足，那我们可以直接利用环境光来实现成像。而当光线较弱，或是特殊情况（比如结构光3D成像，ToF成像，SWIR成像等），Image sensor需要搭配主动光源来使用。对于这样一个系统å，可以参考ESPROS公司的一套工具进行简单的评估设计。
ESPROS是一家位于瑞士的企业，主要研发tof以及LiDAR相关产品，包括芯片，模组，以及整套解决方案（https://www.espros.com）。

![EPC](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data2/EPC.png)

ESPROS网站提供了一套关于TOF的光学系统的简单计算，包括了两个pdf文档和一个excel文件。
https://www.espros.com/downloads/09_Application_notes/AN02_Optical_Power_Calculation/

![fileSummary](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data2/fileSummary.png)

 
下面主要结合“reflected power calculation theory”以及“tof power estimation tool”这两个文件进行学习。

![basic](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data2/basic.png)

基本概念如上图所示，会有一个emitter作为光源，光照射到物体object上，反射回来 的光被sensor接收端所探测。因为这是一个ToF系统，所以有一些基本的假设，比如物体足够远且在光轴的中心线上，可以实现小角度近似，光源可以近似成一个点光源等等。

![emitter_receiver](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data2/emitter_receiver.png)

整个计算包括了两个主要部分，即“物体接受到的光照功率密度”以及“sensor接受到的反射光照功率密度”。

***

## Part #1 “物体接受到的光照功率密度”

由如下公式进行计算：

![Eeo](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data2/Eeo.png)

包括了四个基本项：
- 光源的辐射密度（单位W/sr）:可以结合光源（LED或者VCSEL）的datasheet查看相关信息；
- 光源所照射的立体角（单位sr）：几何光学方面的计算问题，这里面有一个half-angle of the emitter的参数需要理解一下；
- 光源的LENS的透光效率（无量纲）：可以通过模组相关的datasheet找到该参数；
- 光源所照射出来的光斑面积（m2）：几何光学的计算问题，涉及emitter的FOV以及被测物体的距离等信息；

可以结合excel文件了解更详细的求解过程。

![Eeo_table](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data2/Eeo_table.png)

***

## Part #2 “sensor接受到的反射光照功率密度”

由如下公式计算：

![Epixel](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data2/Epixel.png)

包括了以下几个基本项：
•	物体接受到的光照功率密度（单位W/m2）：在Part #1中已经计算出来；
•	物体的反射率（无量纳）：不同的物体反射率变化很大，需要去网上查找相关数据；
•	物体朗伯反射被sensor接收到的效率（无量纲）：几何光学方面的计算问题，这里面涉及朗伯反射，即我们常说的漫反射，需要计算漫反射中有多少能量会被sensor所收集；
•	pixel所对应在物体上的面积（单位m2）：几何光学计算问题，这里结合了sensor镜头的FOV，sensor阵列的行数与列数，拍摄物体的距离等信息进行计算；
•	pixel的面积：（单位m2）：通过sensor的datasheet得知；
•	sensor的LENS的透光效率（无量纲）：可以通过模组相关的datasheet找到该参数；


同样的，可以结合excel文件了解更详细的求解过程：

![Epixel_table](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data2/Epixel_table.png)

***

依靠这个简单的系统模型，在系统参数的确定下可以推算单位时间内有多少光子能够被pixel所接收，从而确定合适的曝光时间。也可以在明确spec的情况下，对模组相关部件进行确定选型。
（excel文件里还有不少关于TOF的干货，有兴趣可以进一步学习）

--END