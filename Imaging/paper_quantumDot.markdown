---
layout: page
title: 
permalink: /imaging/quantum_dot_for_swir_imaging
---

***<font size=6>Quantum Dot for SWIR Imaging</font>***


Nature Electronics从2021 IEDM中选出了一些有比较大突破的报告话题，其中一个即是Quantum dot image sensors scale up，原文链接如下（现在谷粉学术还下不到，大家只能各凭本事去看看了。不过这只是个一页左右的简介，也没啥内容）：
https://doi.org/10.1038/s41928-021-00701-x

做Quantum Dot（QD）来实现Image Sensor的研究机构有不少，一个主要驱动力在于Quantum Dot的禁带宽度可调，针对近红外（NIR）和短波红外（SWIR）的成像有一定的应用前景。特别是SWIR成像，现在成熟的InGaAs器件过于昂贵，而其它技术中，大家相对看好的就是QD来实现SWIR成像，从而将成本降下来。这里有篇综述性质的文章，可以参考着了解大概。
https://sid.onlinelibrary.wiley.com/doi/epdf/10.1002/msid.1257

![Vis_NIR_SWIR](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data1/Vis_NIR_SWIR.png)


Science在2021年也有一篇QD方面的综述文章，<Semiconductor quantum dots: Technological progress and future challenges>，有从材料制备到器件集成，应用等更专业，更全面的介绍。
https://light.utoronto.ca/wp-content/uploads/2021/08/eaaz8541.full_.pdf

在将QD image sensor产品化的道路上走得比较好的且知名的企业和机构主要有IMEC和意法半导体（ST）。当然还有很多小的创业型企业，不过我个人没有了解到特别出彩的商用产品，也没看到重要会议上的论文，所以暂时就不考虑了。

## ST Microelectronics
2021年的IEDM上，意法半导体（ST）发表了相关论文<1.62um Global Shutter Quantum Dot Image Sensor Optimized for Near and Shortwave Infrared>，（论文需要大家自己搞定了，论文部分图示可以在IEDM上看到，ST的官网上也能看到一些内容，另外，作者还在另一个会上发表了文章，说的是同一个事，只是没IEDM文章这么详细全面，可参考High Resolution Quantum Dot Global Shutter Imagers，谷粉学术可下）
https://www.ieee-iedm.org/press-kit
https://blog.st.com/iedm-2021/

ST也是使用了传统的PbS QD材料，PbS QD的尺寸在2nm～20nm之间，能过调节其尺寸可以控制它的吸收峰。将这种QD溶液其旋涂在已经制备好了读出电路的Silicon wafer（并且制备好了QD与Silicon连接的pixel bottom electrode）上并固化，然后去制备共用的top electrode，抗反射层，封闭层等。

![SWIR ST](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data1/ST_QuantumDot.png)

器件的QD大概只有400nm厚（我根据论文图示目测，不一定准确），针对940nm的QE能达到40%+，1400nm的QE能达到60%+，相比于Silicon已经相当高了。同时，论文展示了一些实拍图（ST官网能看到）。

![SWIR imaging](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data1/SWIRsample.png)

论文虽然在性能上或是器件创新上并没有比其它研究机构明显高出一个level或是啥的，但主要出彩的是对工艺的优化（对QD材料保持低氧环境下操作，低温工艺，保护层，光学优化等），对可靠性的测试评估等，以及将其实现在12 inch的wafer上保持高的一致性等。这种量产化的推动可能对目前QD的研究更加重要。ST计划在2022年提供相关demo给潜在客户，并将其大规模量产。论文作者也表示有望将SWIR QD Image Sensor做得像现在Silicon CIS一样的成本，大概一美元这种level，同时，也将进一步push QE，向InGaAs的性能逼近。
https://www.imveurope.com/news/sts-quantum-dot-sensor-set-volume-swir-imaging

![QE](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data1/QE.png)

关于ST做QD image sensor这件事，前几年都没看见相关的论文，好像突然就搞起来了，然后突然就要量产了。不过这次IEDM的文章的作者倒是有多年的QD研究经验，像是初创公司创始人进入ST负责了这个事。另外，有报道表示ST与Nanoco有长期合作来获得QD材料。
https://uk.investing.com/analysis/nanoco-group-making-good-sense-200492932

## IMEC
其实在ST之前，IMEC在更多的大会上发表过关于QD Image Sensor的研究文章，不过可能IMEC还是更偏研究所性质，其产业化没有ST的动作那么快。IMEC于2021年IISW以及2020年IEDM上的都有关于QD image sensor的文章发表：
<Detailed Characterization of SWIR-sensitive Colloidal Quantum Dot Image Sensors>
(https://imagesensors.org/Past%20Workshops/2021%20Workshop/2021%20Papers/R40.pdf)

<Imaging in Short-Wave Infrared with 1.82 μm Pixel Pitch Quantum Dot Image Sensor>


![IMEC_quantumDot](https://raw.githubusercontent.com/betterCallChen/imageData/main/Figures/data1/IMEC_quantumDot.png)

从IEMC的文章可以看出其大致思路和ST的是一致的，都是用PbS QD来实现NIR/SWIR感光，甚至pixel bottom electrode以及公共的top electrode这些特性都一样，pixel pitch也push到了1.82um左右。不过可以发现2021年和2020年是两代不同的产品，其1440nm的QE从原来的13%提升到了40%+。具体的两代产品的迭代可以参考文章<Thin-Film Photodetector Optimization for High-Performance Short-Wavelength Infrared Imaging>(自己想办法)，主要思路是将原来的纯p-type QD升级成p-type QD + n-type QD，这样将耗尽层扩宽，能够有效收集的区域更大了。
更早（大概2017年）的时候，IMEC就开始做QD image sensor了，pixel pitch很大，20um-40um左右，并且还是在3cm x 3cm的玻璃上先做好，然后transfer，一种纯实验室的做法。然后不断迭代才有了2021 IISW中我们所看到的demo样片。（相比于ST，IMEC发表的论文较多，并且有一定的连贯性，可以看到更多的细节）这其中有一个有意思的技术路线，即将QD通过litho实现pixel化（现在看到的pixel都是通过bottom electrode来实现）。IMEC有成功尝试过，不过在最新的demo中又没有使用这个技术。这一点ST也没有做到，可能在材料工程方面还需要进一步研究。

## 未来
ST表示会在2022年开始产业化QD image sensor，让我们拭目以待。
IMEC的研究人员提出了QD image sensor继续发展的一些挑战，比如实现“无铅”材料的QD，从而让更多玩家能接受这种QD器件；比如实现one-step QD的淀积，而不是现在的layer-by-layer的淀积方式；以及可靠性的问题等等。
https://www.imveurope.com/analysis-opinion/quantum-dots-spark-new-swir-wave
关于SWIR成像的应用市场问题，不少人认为这个市场还是特别小众，更多的是在工业/农业检测领域。在消费级产品或是监控上，是否能实现夜视功能，恶劣环境成像，甚至是用于智能驾驶等等，这都有待进一步的市场验证。



--END