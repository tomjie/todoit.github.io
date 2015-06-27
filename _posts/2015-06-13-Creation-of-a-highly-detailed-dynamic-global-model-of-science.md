---
layout: post
title: Creation of a highly detailed, dynamic, global model and map of science笔记(2013)精读
categories:
- informatics
tags:
- 文献计量
- 主题演化
---

##计量学（-metrics），不同的目的需要不同的模型
> 作者：mapofscience.com公司的人
> 
> 发表时间：2013年

##摘要
计量研究（metrics research)目前主要用于解决研究评价的问题，很少用来解决研究计划的（research planning ）问题。该文章基于共引分析的方法，使用16年将近2千万（20million）的数据，构建了篇级的模型和科学地图（article-level and map of science），然后使用该地图对由文献集合构成的学科结构进行定义。将详细和高层次（detail and high-level）的结构结合起来可以解决计划相关的问题，例如识别突发主题、识别科学技术中哪些是创新，哪些只是简单的延续以前的研究（simply persisting）。除了构建模型和地图，还详细说明了如何改进方法从而使得学科结构更加精确，包括使用文献耦合方法将当前的论文分配到共引聚类中，<del>以及通过混合方法生成模型的可视化地图</del>(不需要看)。

##引言
当前的计量学研究如火如荼，科学计量学（sciento-metrics）、文献计量学（biblio-metrics）、信息计量学（infor-metrics）、替代计量学（alt-metrics）等等，但是这样研究主要用于评价(
[Science and technology studies: Exploring the knowledge base. Research Policy](http://www.sciencedirect.com/science/article/pii/S0048733312000716) [[下载] (http://digital.csic.es/butitstream/10261/35242/1/Martin%20Nightingale%20Yegros%20DIME%202011.pdf)]，例如影响因子，H指数、大学排名、国家级的科学指标等等。使用基于文献的指标进行演讲评价已经有40多年的历史，一些文献计量期刊、会议等等都说明该领域已经发展很快，因此使用科技文献进行研究评价的领域已经很成熟。

但是在研究计划领域，计量学研究就相对较少，计划相关的问题([An Introduction to Modeling Science: Basic Model Types, Key Definitions, and a General Framework for the Comparison of Process Models](http://link.springer.com/chapter/10.1007/978-3-642-23068-4_1))不用于评价问题，而且被基金资助者、管理者和研究人员所关注，因此，需要不同于评价方法的模型。例如
> - 计划可能更需要新兴主题的发现和识别模型；
> - 基金资助者可能需要模型帮助他们识别最具创新和有价值的研究课题和研究人员；
> - 管理者，尤其是产业界的管理者，可能需要模型帮助他们更好的分配内部研究资金，包括了解哪个正在研究的领域需要被砍掉。

为了实现更详细的计划，科技领域基于文档的模型必须被高度细粒度化，同时基于回顾性数据时，数据必须足够强健从而保证预测的可靠性。在计量学领域中，研究和开发这样的模型目前进展较慢。

 
##背景

科学地图，需要有两个部分，即分类和可视化。之前的大部分研究都是根据文档、期刊和作者进行粗略的分类，然后用基于文本和基于引文的方法。关于这些方法的综述有很多。
这些不同的方法都用于回答特定的问题：

> - 基于作者的方法主要用来描述一个研究领域的主要主题，并找出该领域的主要研究者。
> - 基于期刊的方法通常通常用户描述科学中学科层的结构，基于期刊的Overlay maps可以回答高层的政策问题；

但是，更详细的问题，例如计划相关的问题，要求使用文档级别的模型来解释科学地图。目前的方法在文档级别上大都使用本地较小的数据集，而没有使用整个数据集，但是使用整个数据集可以增加精度。

###引文分析的历史

20世纪70年代的文档级别的全景科学地图：
> - 第一个基于文档的全球范围的科学地图由Griffith，Small，Stonehill & Dey在1974年创建。[The structure of scientific literatures II: Toward a macro-and microstructure for science](http://sss.sagepub.com/content/4/4/339.full.pdf)，该地图使用共引分析方法，将文献集合聚成115个类，并从中找到1310个高被引文献，战士了生物医学、物理学和化学领域中最高被引的领域。

> - Henry Small在1985年继续使用共引分析生成文档级别的地图，并首先使用了具有代表性的学科分区引文阈值，结束了粗略使用top1%高被引的方法。 [Clustering the Science Citation Index using co-citations ](Clustering the science citation index® using co-citations)。 同时，Small在美国科学信息研究所（ISI）简历的潜逃的四个级别科学地图软件。

> - Small 在1999年基于1995年发表的13万篇高被引文献提出了四层地图，在地图的最低层，有19000个类。[Visualizing science by citation mapping](http://web.simmons.edu/~benoit/lis466/visdoc/ProQuest_43241275.pdf)，同时Center for Reserch Planning也创建了相似的地图，主要区别在于CRP仅仅使用了聚类层。

构建全景科学地图的第二个阶段发生在21世纪：
> - Klabans & Boyack在2006年创建了共引模型和文献耦合模型。[Quantitative evaluation of large maps of science] (http://link.springer.com/article/10.1007/s11192-006-0125-x)

> - Boyack在2008年使用文献耦合创建了模型和科学地图。[Using detailed maps of science to identify potential collaborations](http://www.akademiai.com/index/N2773232222R7012.pdf)

> - 在2004年之前，用于构建科学地图的主要数据源是ISI，但是2004年之后，Scopus数据库被引入，Scopus成为另一个用于分析科学地图的数据源。

> 2020年，Klavans & Boyack使用Scopus数据创建了共引模型。


**上述所有的方法都是静态地图，主要是由于数据来自于单一的年份，或者科学地图快照生成在特定的时间点，近几年开始，科学家才开始创建动态的地图。**

> - 2011年，Klavans & Boyack使用共引分析方法将9年（2000-2008）的科学模型连接到一起。[Using global mapping to create more accurate document- level maps of research fields](http://onlinelibrary.wiley.com/doi/10.1002/asi.21444/full)

> - 2012年，CWTS的Waltman & van Eck使用直接引文和基于模块的方法对 web of science 上2001-2010年将近1000万数据进行聚类，该方法和VOS方法类似，该方法和其他方法相比有许多优点：
	- 可以生成多层的聚类结果；
	- 可以处理非常大的文档集合；
	- 该方法既然在直接引文中可以使用，当然在其他的方法比如共引、文献耦合或者混合相似度即使中也可以使用。
   
##对共引模型和构建科学地图方法的改进

作者使用共引分析方法已经很多年，是因为共引分析方法有比较出色的几个特征，即**共引分析的优点**：

 > - 共引分析生成的聚类足够精确。 [Co-citation analysis, bibliographic coupling, and direct citation: Which citation approach represents the research front most accurately?](http://onlinelibrary.wiley.com/doi/10.1002/asi.21419/full)

 > - 共引分析可以对最新的论文进行分类，因此可以通过最新论文的重叠建立之前共引构建的类之间的链接。[Toward an objective, reliable and accurate method for measuring research leadership](http://link.springer.com/article/10.1007/s11192-010-0188-6)

 > - 在概念层，共引分析的模型的认知结构趋向于高度**不稳定**，[Citation data as science indicators]()，对于用于识别早期的突发现象来说，不稳定性是一个非常有用的特征。

 > - 对于纵向连接不同时间段的年度类来说，共引聚类中的参考文献是重要并且准确的基础，可以用来探测科学的动态结构。[Using global mapping to create more accurate document- level maps of research fields](http://onlinelibrary.wiley.com/doi/10.1002/asi.21444/abstract?deniedAccessCustomisedMessage=&userIsAuthenticated=false)



一般来说，共引分析主要有两个阶段：（1）将参考文献分到共引类簇中；（2）将当前的论文分入到共引类簇中。为了使得共引模型的结果更加精确，作者在三个方面进行了改进。

--未完待续--

 

#### **1 共引阈值**

  以前一些研究的共引阈值选择的都比较高，例如1%，其目的是为了聚焦到科学领域最热门的研究领域，作者使用了较低的阈值，因为其目的是为了发现热门研究领域之外的平均水平甚至是冷门研究领域。

  作者使用了6个不同的数据集进行测试，首先进行聚类，然后使用其方法对文本连贯性（textual coherence）进行测度，如果该类的词越相关，则该类就越精确，相关性通过JS距离（Jensen-Shannon divergence）来测度，该测度方法用来计算两个概率分布的距离，在该文中，作者通过计算每个文档中词的概率分布与其所在类的词的概率分布来计算，步骤如下：

 

 - （1）计算所有文档与其所在类的JSD的平均值

 - （2）因为JSD距离和类簇的大小相关，要计算相关性就要进行标准化（标准化的方法没看懂）

 - （3）计算整个数据集的相关性。

 

 经过测试，CCA-STS各指标得分最优。

 

#### 2 将文献耦合应用到当前论文分配中

 由于共引方法和文献耦合相比，其类的相关性较低。

 作者觉得在第二步，即当前论文分配中存在问题，造成其相关性低，然后希望使用文献耦合来进行当前论文分配。

 #### 3 构建可视化Map

