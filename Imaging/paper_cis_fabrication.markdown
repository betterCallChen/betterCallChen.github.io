---
layout: page
title: 
permalink: /imaging/cis_process_introduction
---

***<font size=6>Fabrication of CMOS Image Sensor</font>***


序：记录下CIS的制造工艺（以普通的RGB image sensor为例）方面较基础的笔记。

## 1. TO之前
### 1.1 FSI与BSI
在设计一款CIS之前，从工艺的角度，最先需要做出选择的可能就是FSI（front-side illumination）还是BSI（back-side illumination）。
 
(From Sony)
FSI和基础的CMOS logic工艺一样，首先完成前道工艺（FEOL，front-end-of-line），然后做后道工艺（BEOL，back-end-of-line），最后在表面做光学模块（color filter以及micro-lens）。FSI的一个主要问题在于光进入到silicon之前需要穿过较厚的金属布线层，这导致了较多的光子损失，影响了最终的量子效率（QE，quantum efficiency）。特别是像素不断缩小，有效的感光面积占整个pixel的区域变得更加有限。
BSI即是为了解决这个问题而发明，BSI在完成BEOL之后，会将sensor wafer（wafer #A）翻转过来，然后将其bonding到另一个wafer（wafer #B，carrier wafer）上，从背面开始将wafer #A减薄，直到wafer #A只剩下器件需要的厚度（比如3um左右）。然后再在表面去做color filter和micro-lens。这样，在BSI工艺中，光从背面可以直接入射到silicon中，而不需要经过金属布线层，因此对于小像素而言，其QE能得到较大提升。
BSI比较关键的技术点包括wafer的键合技术，背面减薄技术，背面PAD技术（BSI工艺细节时再讲）。
在BSI技术量产之前，FSI还有一个演进技术，即使用light-pipe技术，也称为light-guide技术。该技术还是基于FSI，在Photodiode的上方的金属布线层中加入高介质材料，利用全反射原理来减小光的损失，如下图示。这条技术路线比较冷门，详细内容以后有机会再整理。
 
(From EEWEB)
### 1.2 Stacking技术
BSI进一步发展出了stacking技术，即将sensor与logic分别制造在不同的wafer中，这样sensor wafer被bonding在logic wafer上被减薄。stacking的优势在sensor wafer的工艺可以单独优化，不必受限于logic wafer的工艺；而且，能够将整个sensor面积做得更小，或是说同样的面积能够集成更复杂的功能（比如event-based camera，SPAD camera，AI-included sensor等sensor的发展，都很大程度受益于stacking技术）。而stacking技术比较关键的技术点除了BSI的相关技术外，还需要考虑两个wafer之间的电气连接问题。在这一点上，主要有两个解决方案：TSV（硅穿孔技术）以及Cu-Cu direct bonding（有时也叫hybrid bonding）。这一方面要展开的话有较多的内容，在以后的笔记中再详细说明。可以参考2017和2019 IISW里techInsights的综述文章<参考文献1，2>：
 
(From Sony)

在Stacking上进一步发展，可以由传统的double-stacking演变成triple stacking。这个目前量产产品有在Sony和Samsung见到过。
 
(From Sony)

triple stacking一般是额外加了一个DARM，不过Sony在最新2021 IEDM会议上还提出了一种新的triple-stacking方式，即将pixel section单独再拆成两个wafer。
 
(From Sony)

就FSI与BSI的选择问题，除了综合产品spec以及成本方面的考虑，FAB相关工艺的成熟度也是很重要的一个考虑。就大陆FAB厂而言，有些FAB虽然有成熟的CIS产线，但不一定支持BSI工艺，而Stacking的工艺要求就更难了。
### 1.3 Technology Node
相对logic芯片，CIS对于工艺节点的要求并没有那么高。目前看到的产品，0.13um的工艺都有可能在使用。当然，我们从主流手机使用的CIS来看，sensor wafer主要还是在90nm/65nm/40nm，logic wafer则主要是65nm/40nm等。对于Samsung而言，它有些高端产品在logic wafer上会使用自家的28nm high-k工艺。
 
(2017 IISW, TechInsights)

虽然CIS对于工艺节点的推进没有很激进，但也能看到最新的趋势是logic wafer朝28nm推进（集成更多功能，更低功耗等优势），Sony，TSMC以及Samsung是在这方面走在比较前面的。更激进的技术也有在这些大厂的ppt中提及，但相对没那么成熟，客户的需求度可能也没那么高。对于手机上使用的CIS，其像素尺寸小，面阵大，对工艺节点要求会略高一些。
根据最新的消息，Sony和TSMC的深度合作，在工艺结点上有进一步push，甚至在sensor wafer也将使用更高级的节点。Samsung则在2019 IEDM上有发表使用FinFET在CIS中，在2021年的roadmap中也提到相关展望。
 
(From Yahoo, Samsung)

Technology Node的选择也是性能成本等的综合考虑，没有特殊原因一般都跟着主流/竞品走就行了。
### 1.4 Raw wafer
现在主流的CIS wafer都是在用高阻epi wafer，器件制备在高阻epi层（阻值量级为10 Ohm-cm），epi的厚度大概在6um左右（vendor一般会有几个常见厚度供选择，如果要定制厚度，发货周期可能会稍微长一点），而Substrate的阻值会低一点，大概0.05 Ohm-cm这种量级。
如果需要特殊定制wafer，则主要通过Fab与wafer vendor去谈。
## 2. TO
### 2.1 Short Loop
一般而言，如果FAB有成熟的CIS产线且能符合要求的话，那就不用谈太多。了解它的process flow，画好版图TO就行了。不过如果需要开发一些单点工序，则需要留够时间和FAB安排相关的short loop实验，小流程跑通了再跑完整的process flow。这种需要和FAB有较多的磨合（钱也要砸进去不少）。具体的项目也不一样，没法统一说要怎么做，只能靠经验去把握了。但是一个重要的原则就是尽可能提前，因为项目delay是一种常态。

### 2.2 FEOL
前道工序与传统的CMOS工艺没有太多区别，这也是CIS能够战胜CCD，做到很低成本的一个重要原因。大致的工序包括：（AA/STI工序）>（各种Well implant）> （各种Pixel相关的implant）>（Gate Oxide工序）>（Poly Gate工序）>（OFFSET工序）>（LDD注入）>（SPACER工序）>（源漏注入）>（ESD注入工序）>（Salicide工序）>（CESL工序）>（Pre-metal介质层）
具体的每道工序以及thermal相关的东西，在各家的Fab以及不同的工艺节点都会有所区别，但基本思路不会有大的变动。
这里对于CIS而言，主要有几个地方可能需要注意：
- Gate-Oxide的厚度：因为Pixel内的读出管通常是使用2.7-3.3V这种电压，与logic电路中的core device不一样，因此一般pixel内是需要用thick gate oxide，可以与IO管一样，也可以根据自己的条件选择合适的thickness（但是会需要额外的工序以及Mask）。
- Source Follower部分：Source Follower部分对于CIS的噪声贡献较大，所以通常会想要对SF进行一些优化操作，包括了Fluorine implant，thinner gate oxide等等。DB Hitek有几篇比较好的文章对SF的优化工艺进行了分析说明（参考文献3，4）。
- 源漏注入：有些logic工艺中，源漏注入会有Ge的掺杂。但是对于Pixel区域，应当避免Ge掺杂，如果有必要，需要有Pixel单独的源漏注入。
- Salicide部分：Pixel区域是不进行salicide的，因此做道工序时要注意将pixel array全部保护住。

### 2.3 BEOL
前道工序完成后，接下来会进行后道工序，即金属布线层。
这一段没有太多可操作的，Fab的工艺流程都是相对固定的。根据工艺线的不同，现阶段有些是使用的Al工艺，有些使用的是Cu工艺。这些和传统CMOS工艺一致。

### 2.4 BSI工艺
如果是FSI，那在BEOL完成后就进行光学模块的制备。不过目前主流还是BSI工艺（包括Stacking），所以在进行光学模块之前，还需要完成BSI工艺。
BSI工艺包括了如下几个步骤：（翻转后Bonding）>（背面减薄工序）>（DTI工序）>（HK film工序）>（Metal Grid工序）> （开PAD工序）
翻转后bonding一般是利用两片wafer均长一层薄薄的oxide，然后通过oxide bonding到一块。不过现在更先进的Cu-Cu direct bonding技术（也叫hybrid bonding技术），工序会有区别，这点以后再详细分析。
背面减薄工序一般是利用grinding进行快速研磨减薄（不需要高精度的控制，将wafer从初始的750um左右厚减薄到几十um厚左右），然后利用wet etchant（比如HNA）进行湿法刻蚀减薄（这一步通常会利用wafer的epi与substrate之间的浓度差实现高的选择比，从而精确地将substrate全部去除，而留下epi部分）。之后可能还会进行一些CMP操作以及湿法刻蚀来进一步细调处理。
 
(From Google Search)

DTI是指deep trench isolation，这个工序不是必须的，但对于小像素sensor的像素间隔离十分重要。理想情况就是将pixel之间完全隔离（光学隔离&电学隔离），但考虑实际工艺情况以及成本，比如trench的深宽比，trench的填充问题，trench侧壁的passivation等等问题，普通的DTI通常并没有将silicon刻穿，DTI的内部填充则主要由silicon oxide填充实现。DTI的实际工艺会有更多种选择，也在以后的笔记中再详细分析。
HK film在有些描述中也叫AR coating，即Anti-reflection coating。通常由AlO/HfO，TaO等材料实现的薄膜（总共几十nm厚左右）。除了在光学层面有抗反射的作用，在电学上，还能提供负电荷，起到对背面（经历了背面减薄）以及DTI侧壁（经历了深槽刻蚀）的保护，降低暗电流。注意DTI的里面也要铺一层HK film，所以这道工序是在DTI的填充之前进行。
 
(From 2015 IISW, TechInsights)

Metal Grid工序，Metal Grid是在pixel周围的一圈金属，用来降低光学上的crosstalk，通常用W材料来做metal grid。不过最新的技术是使用composite (metal + oxide) grid，甚至是metal-free grid。
 
(From OV 2018 paper, doi:10.3390/s18020667, open access)

开PAD工序，在完成前面的所有工序并实现平坦化后，需要将芯片的PAD露出来。这部分工序是首先将PAD处的silicon完全刻蚀掉，然后将介质层刻蚀掉，这样可以露出BEOL中的Metal层。理论上M1暴露出来即可，不过有些FAB也会选择将Top metal暴露。接下来淀积Al并图形化刻蚀，只保留PAD附近的Al即可。这部分Al通过前面暴露出来的BEOL中的metal层直接接触，实现电气连接。后面可以考虑再加一层oxide将芯片都保护住，只留PAD这一小部分开口用于后续封装。开PAD这部分工序有一些细节需要注意，比如曝光的控制，比如PAD与silicon之间的电气隔离等，这里的工序出问题会直接导致芯片彻底废掉，完全测不到东西，所以需要特别小心。
 
(From Brillnics 2020 paper, doi.org/10.3390/s20020486, open access)

## 3. 光学模块工艺
光学模块这部分主要是color filter和micro lens的制备，这一部分并不是由image sensor的fab做的，而是拿到外面其它厂商去做（比如大陆的TSES以及台湾的VisEra，虽然它们分别与SMIC和TSMC有很深的关系，但是它们也是对外接其它FAB的单子的）。从工艺的角度这一块没有太多可说的，一般照着fab的工序做就是了，只是需要提供它们一些MASK信息，以及一些设计参数。目前主流的color filter还是RGB的Bayer阵列以及它的一些变形衍生，比如quad-bayer，nonacell，RYYB等技术。后续再有机会详细记录下这一块的工艺步骤以及前研的研究。
做完光学模块，基本就okay了。后续的切割，封装，测试等就是另一大块领域了，以后接触学习了解更多了再总结。

## 4. Reference 
[1] “A Survey of Enabling Technologies in Successful Consumer Digital Imaging Products”

<https://www.imagesensors.org/Past%20Workshops/2017%20Workshop/2017%20Papers/R06.pdf>

[2] “The State-of-the-Art of Smartphone Imagers”

<https://www.imagesensors.org/Past%20Workshops/2019%20Workshop/2019%20Papers/R01.pdf>

[3] “Temporal Noise Improvement Using the Selective Application of the Fluorine Implantation in the CMOS Image Sensor”

<https://www.imagesensors.org/Past%20Workshops/2017%20Workshop/2017%20Papers/R09.pdf>

[4] “Several Process Techniques & Pixel Source Follower Schemes to improve the Pixel Temporal Noise ”

<https://www.imagesensors.org/Past%20Workshops/2019%20Workshop/2019%20Papers/R08.pdf>

--END