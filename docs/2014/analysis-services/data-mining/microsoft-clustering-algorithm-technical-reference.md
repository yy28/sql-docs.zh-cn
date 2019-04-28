---
title: Microsoft 聚类分析算法技术参考 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- clustering [Data Mining]
- MAXIMUM_INPUT_ATTRIBUTES parameter
- CLUSTER_SEED parameter
- MODELLING_CARDINALITY parameter
- MINIMUM_SUPPORT parameter
- STOPPING_TOLERANCE parameter
- MAXIMUM_STATES parameter
- SAMPLE_SIZE parameter
- CLUSTERING_METHOD parameter
- soft clustering [Data Mining]
- clustering algorithms [Analysis Services]
- CLUSTER_COUNT parameter
ms.assetid: ec40868a-6dc7-4dfa-aadc-dedf69e555eb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3bf6919230c1621d2b81eb41cd715fc1878a90c5
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62721879"
---
# <a name="microsoft-clustering-algorithm-technical-reference"></a>Microsoft 聚类分析算法技术参考
  本节说明 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法的实现，包括可用来控制聚类分析模型的行为的参数。 还提供关于在创建和处理聚类分析模型时如何提高性能的指南。  
  
 有关如何使用聚类分析模型的其他信息，请参阅下列主题：  
  
-   [聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
-   [聚类分析模型查询示例](clustering-model-query-examples.md)  
  
## <a name="implementation-of-the-microsoft-clustering-algorithm"></a>Microsoft 聚类分析算法的实现  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法提供两种创建分类并为分类分配数据点的方法。 第一种方法是 *K-means* 算法，这是一种较难的聚类分析方法。 这意味着一个数据点只能属于一个分类，并会为该分类中的每个数据点的成员身份计算一个概率。 第二种方法是期望值最大化 (EM) 方法，这是软聚类分析方法。 这意味着一个数据点总是属于多个分类，并会为每个数据点和分类的组合计算一个概率。  
  
 可以通过设置 *CLUSTERING_METHOD* 参数来选择要使用的算法。 聚类分析的默认方法是可缩放的 EM。  
  
### <a name="em-clustering"></a>EM 聚类分析  
 在 EM 聚类分析中，此算法反复优化初始分类模型以适合数据，并确定数据点存在于某个分类中的概率。 当概率模型适合于数据时，此算法终止这一过程。 用于确定是否适合的函数是数据适合模型的对数可能性。  
  
 如果在此过程中生成空分类，或者一个或多个分类的成员身份低于给定的阈值，则具有低填充率的分类会以新数据点重设种子，并且 EM 算法重新运行。  
  
 EM 聚类分析方法的结果是概率性的。 这意味着每个数据点都属于所有分类，但数据点向分类的每次分配都有一个不同的概率。 因为此方法允许分类重叠，所以所有分类中的项的总数可能超过定型集中的总项数。 在挖掘模型结果中，指示支持的分数会相应地调整以说明这一情况。  
  
 EM 算法是 Microsoft 聚类分析模型中使用的默认算法。 此算法之所以用作默认算法，是因为与 k-means 聚类分析算法相比，它有多个优点：  
  
-   最多需要一次数据库扫描。  
  
-   工作时不受内存 (RAM) 限制。  
  
-   能够使用只进游标。  
  
-   优于抽样方法。  
  
 Microsoft 实现提供两个选项：可缩放 EM 和不可缩放 EM。 默认情况下，在可缩放 EM 中，前 50,000 个记录用于为初始扫描设种子。 如果成功，则模型将仅仅使用这些数据。 如果使用 50,000 个记录时模型不适合，则会继续读取 50,000 个记录。 在不可缩放 EM 中，总是读取整个数据集，而不考虑数据集的大小。 此方法可能会创建更准确的分类，但内存需求非常高。 因为可缩放 EM 作用于本地缓冲区，所以循环访问数据要快得多，并且此算法对 CPU 内存缓存的利用率比不可缩放 EM 要高得多。 此外，可缩放 EM 比不可缩放 EM 快三倍，即使所有数据都可容纳于主内存中也是如此。 在大多数情况下，性能改进不会导致完成的模型的质量下降。  
  
 有关介绍 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法中的 EM 的实现的技术报告，请参阅 [Scaling EM (Expectation Maximization) Clustering to Large Databases](https://go.microsoft.com/fwlink/?LinkId=45964)（针对大数据库对 EM (Expectation Maximization) 聚类分析进行扩展）。  
  
### <a name="k-means-clustering"></a>k-means 聚类分析  
 k-means 聚类分析是一种广为人知的方法，它通过尽量缩小一个分类中的项之间的差异，同时尽量拉大分类之间的距离，来分配分类成员身份。 k-means 中的 "means" 指的是分类的“中点”，它是任意选定的一个数据点，之后反复优化，直到真正代表该分类中的所有数据点的平均值。 "k" 指的是用于为聚类分析过程设种子的任意数目的点。 k-means 算法计算一个分类中的数据记录之间的欧几里得距离的平方，以及表示分类平均值的矢量，并在和达到最小值时在最后一组 k 分类上收敛。  
  
 k-means 算法仅仅将每个数据点分配给一个分类，并且不允许成员身份存在不确定性。 分类中的成员身份表示为与中点的距离。  
  
 通常，k-means 算法用于创建连续属性的分类，在这种情况下，计算与平均值的距离非常简单。 但是， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 实现通过使用概率针对分类离散属性对 k-means 方法进行改编。  对于离散属性，数据点与特定分类的距离按如下公式计算：  
  
 1 - P(数据点, 分类)  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法不公开用于计算 k-means 的距离函数，并且在完成的模型中不能测量距离。 但是，可以使用预测函数返回与距离对应的值，在这种情况下，距离计算为某个数据点属于此分类的概率。 有关详细信息，请参阅 [ClusterProbability (DMX)](/sql/dmx/clusterprobability-dmx)。  
  
 k-means 算法提供两种对数据集进行抽样的方法：不可缩放的 K-means 和可缩放的 k-means，前者加载整个数据集并创建一个聚类分析阶段，后者使用前 50,000 个事例，并仅仅在需要更多数据才能使模型很好地适合数据时读取更多事例。  
  
### <a name="updates-to-the-microsoft-clustering-algorithm-in-sql-server-2008"></a>在 SQL Server 2008 中对 Microsoft 聚类分析算法的更新  
 在 SQL Server 2008 中， [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法的默认配置已更改为使用内部参数 NORMALIZATION = 1。 使用 z-score 统计信息执行规范化，并且假定正态分布。 默认行为中的这一更改旨在尽量减小可能具有很大量度和许多离群值的属性的影响。 但是，z-score 规范化可能会更改针对并非正态的分布（例如均匀分布）的聚类分析结果。 为了避免规范化和获取与 SQL Server 2005 中的 K-means 聚类分析算法相同的行为，可以使用“参数设置”对话框添加自定义参数 NORMALIZATION 并将其值设置为 0。  
  
> [!NOTE]  
>  NORMALIZATION 参数是 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法的内部属性并且不受支持。 通常，建议在聚类分析模型中使用规范化以便改进模型结果。  
  
## <a name="customizing-the-microsoft-clustering-algorithm"></a>自定义 Microsoft 聚类分析算法  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法支持几个参数，这些参数会影响所生成的挖掘模型的行为、性能和准确性。  
  
### <a name="setting-algorithm-parameters"></a>设置算法参数  
 下表介绍可与 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法一起使用的参数。 这些参数影响生成的挖掘模型的性能和准确性。  
  
 CLUSTERING_METHOD  
 指定算法要使用的聚类分析方法。 有下列聚类分析方法可用：  
  
|ID|方法|  
|--------|------------|  
|1|可缩放 EM|  
|2|不可缩放 EM|  
|3|可缩放 k-means|  
|4|不可缩放 k-means。|  
  
 默认值为 1（可缩放 EM）。  
  
 CLUSTER_COUNT  
 指定将由算法生成的大致分类数。 如果无法基于相应的数据生成该大致数目的分类，则算法将生成尽可能多的分类。 如果将 CLUSTER_COUNT 设置为 0，则算法将使用试探性方法最准确地确定要生成的分类数。  
  
 默认值为 10。  
  
 CLUSTER_SEED  
 指定在为建模初始阶段随机生成分类时所要使用的种子数量。  
  
 通过更改此数字，可以更改生成初始分类的方法，然后使用不同的种子比较已生成的模型。 如果种子已更改，但所发现的分类并没有太大的更改，则模型可被视为相对稳定。  
  
 默认值为 0。  
  
 MINIMUM_SUPPORT  
 指定生成某个分类至少需要的事例数。 如果分类中的事例数小于此数目，则此分类将被视为空，并将被丢弃。  
  
 如果将这个数目设置得过高，则可能遗漏有效分类。  
  
> [!NOTE]  
>  如果使用 EM，即默认聚类分析方法，则一些分类可能具有低于指定值的支持值。 这是因为会计算每个事例在所有可能分类中的成员身份，对于某些分类，可能仅存在最小支持。  
  
 默认值为 1。  
  
 MODELLING_CARDINALITY  
 指定在聚类分析过程中构建的示例模型数。  
  
 减少候选模型数会提高性能，但存在遗漏一些好的候选模型的风险。  
  
 默认值为 10。  
  
 STOPPING_TOLERANCE  
 指定一个值，它可确定何时达到收敛而且算法完成建模。 当分类概率中的整体变化小于 STOPPING_TOLERANCE 参数与模型大小之比时，即达到收敛。  
  
 默认值为 10。  
  
 SAMPLE_SIZE  
 如果 CLUSTERING_METHOD 参数设置为其中一个可缩放聚类分析方法，请指定算法在每个传递中使用的事例数。 如果将 SAMPLE_SIZE 参数设置为 0，则会在单个传递中对整个数据集进行聚类分析操作， 在单个传递中加载整个数据集会导致内存和性能问题。  
  
 默认值为 50000。  
  
 MAXIMUM_INPUT_ATTRIBUTES  
 指定算法在调用功能选择之前可以处理的最大输入属性数。 将该值设置为 0 表示不限制属性的最大数目。  
  
 增大属性的数目会大大降低性能。  
  
 默认值为 255。  
  
 MAXIMUM_STATES  
 指定算法支持的最大属性状态数。 如果属性的状态数超过此最大值，则算法将使用最常见状态，而忽略其余状态。  
  
 增大状态的数目会大大降低性能。  
  
 默认值为 100。  
  
### <a name="modeling-flags"></a>建模标志  
 此算法支持下列建模标志。 在创建挖掘结构或挖掘模型时会定义建模标志。 建模标志指定在分析过程中如何处理每一列中的值。  
  
|建模标志|Description|  
|-------------------|-----------------|  
|MODEL_EXISTENCE_ONLY|该列将被视为具有两个可能状态：Missing 和 Existing。 Null 表示缺失值。<br /><br /> 适用于挖掘模型列。|  
|NOT NULL|此列中不能包含 Null 值。 如果 Analysis Services 在模型定型过程中遇到 Null 值，将会导致错误。<br /><br /> 适用于挖掘结构列。|  
  
## <a name="requirements"></a>要求  
 聚类分析模型必须包含一个键列和若干输入列。 还可以将输入列定义为可预测列。 设置为 `Predict Only` 的列不用来生成分类。 在生成分类后，将计算这些值在分类中的分布。  
  
### <a name="input-and-predictable-columns"></a>输入列和可预测列  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 聚类分析算法支持下表中列出的特定输入列和可预测列。 有关内容类型在用于挖掘模型中时的含义的详细信息，请参阅[内容类型（数据挖掘）](content-types-data-mining.md)。  
  
|“列”|内容类型|  
|------------|-------------------|  
|输入属性|连续、循环、离散、离散化、键、表和已排序|  
|可预测属性|连续、循环、离散、离散化、表和已排序|  
  
> [!NOTE]  
>  支持 Cyclical 和 Ordered 内容类型，但算法会将它们视为离散值，不会进行特殊处理。  
  
## <a name="see-also"></a>请参阅  
 [Microsoft 聚类分析算法](microsoft-clustering-algorithm.md)   
 [聚类分析模型查询示例](clustering-model-query-examples.md)   
 [聚类分析模型的挖掘模型内容（Analysis Services - 数据挖掘）](mining-model-content-for-clustering-models-analysis-services-data-mining.md)  
  
  
