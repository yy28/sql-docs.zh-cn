---
title: "分区 (Analysis Services-多维数据) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- incremental updates [Analysis Services]
- data sources [Analysis Services], partitions
- data storage [Analysis Services]
- aggregations [Analysis Services], partitions
- OLAP objects [Analysis Services], partitions
- storing data [Analysis Services], partitions
- partitions [Analysis Services], about partitions
- cubes [Analysis Services], partitions
- partitions [Analysis Services]
- remote partitions [Analysis Services]
- measure groups [Analysis Services], partitions
ms.assetid: cd10ad00-468c-4d49-9f8d-873494d04b4f
caps.latest.revision: 
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 1a44581e828d92756c46b897d9e7c9be69144c5b
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2018
---
# <a name="partitions-analysis-services---multidimensional-data"></a>分区（Analysis Services - 多维数据）
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
分区是一部分度量值组数据的容器。 从 MDX 查询是看不到分区的，任何查询反映的均是度量值组的全部内容，这与为度量值组定义的分区数量无关。 分区的数据内容由分区的查询绑定和切片表达式定义。  
  
 简单 <xref:Microsoft.AnalysisServices.Partition> 对象由基本信息、切片定义、聚合设计等组成。 基本信息包括分区的名称、存储模式和处理模式等。 切片定义是指定元组或集的 MDX 表达式。 切片定义具有的限制与 StrToSet MDX 函数相同。 借助 CONSTRAINED 参数，切片定义可使用多维数据集中的维度、层次结构、级别和成员名称、键、唯一名称或其他命名对象，但不能使用 MDX 函数。 聚合设计是可由多个分区共享的聚合定义的集合。 默认聚合设计取自父多维数据集的聚合设计。  
  
 通过使用分区[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以管理和多维数据集中存储数据和聚合的度量值组。 每个度量值组至少有一个分区；该分区在定义度量值组时创建。 为度量值组创建新分区时，该新分区将添加到此度量值组已有的分区集合中。 度量值组反映了其所有分区中所包含的组合数据。 这意味着必须确保度量值组中某分区的数据不同于此度量值组中任何其他分区的数据，从而确保未在度量值组中多次反映此数据。 度量值组的原始分区基于多维数据集的数据源视图中的单个事实数据表。 当度量值组有多个分区时，每个分区可以引用数据源视图中的或者多维数据集的基本关系数据源中的不同表。 如果将每个分区限制到表中的不同行，则度量值组中的多个分区可以引用同一个表。  
  
 分区是用来管理多维数据集（尤其是大型多维数据集）的强大而灵活的工具。 例如，某个包含销售信息的多维数据集可以包含存储过去每一年数据的分区和存储当年每一季度数据的分区。 将当前信息添加到多维数据集时，只需处理当前季度分区；如果处理的数据量越少，则会通过缩短处理时间来提高处理性能。 在年末，这四个针对季度的分区可以合并成一个单独的针对全年的分区，并为新一年的第一季度创建新分区。 此外，该新分区的创建过程可以作为数据仓库加载和多维数据集处理过程的一部分自动执行。  
  
 分区对多维数据集的业务用户不可见。 但是，管理员可以配置、添加或删除分区。 每个分区都存储在一组单独的文件中。 每个分区的聚合数据都可以存储在定义该分区的 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中，也可以存储在其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中，或者存储在用于提供分区的源数据的数据源中。 分区允许多维数据集的源数据和聚合数据分布在多个硬盘驱动器和多个服务器计算机中。 对于中型到大型的多维数据集而言，分区可以极大地提高查询性能、负载性能和多维数据集的易维护性。  
  
 可以在独立于度量值组中其他分区的情况下，对每个分区的存储模式进行配置。 可以使用源数据位置、存储模式、主动缓存和聚合设计的选项的任意组合来存储分区。 在设计分区时，您可以使用实时 OLAP 和主动缓存的选项来平衡查询速度以避免发生滞后。 存储选项还可以应用于相关的维度以及度量值组中的事实。 这种灵活性使您能够按照需要设计多维数据集的存储策略。 有关详细信息，请参阅[分区存储模式和处理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)，[聚合和聚合设计](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md)和[主动缓存 &#40;分区 &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="partition-structure"></a>分区结构  
 分区的结构必须与其度量值组的结构匹配，这意味着还必须在分区中定义用于定义度量值组的度量值以及所有相关维度。 因此，创建分区时，它将自动继承为度量值组定义的同一组度量值和相关维度。  
  
 但是，度量值组中的每个分区可以有不同的事实数据表，并且这些事实数据表可以来自不同的数据源。 当度量值组中的不同分区有不同的事实数据表时，这些表必须非常相似以维护度量值组的结构，这意味着处理查询会针对所有分区的所有事实数据表返回相同的列和数据类型。  
  
 如果不同分区的事实数据表来自不同的数据源，则任何相关维度的源表和任何中间事实数据表还必须包含在所有数据源中，并且它们在所有数据库中的结构必须相同。 而且，在定义与度量值组相关的多维数据集维度的属性时，需要使用的所有维度表列都必须包含在所有数据源中。 如果分区源表与度量值组的源表有相同的结构，则不需要定义分区的源表和相关维度表之间的所有联接。  
  
 有些事实数据表可能会包含未用于定义度量值组中度量值的列，但有些则不会包含。 同样，有些数据库可能会包含未用于定义相关维度表中属性的列，但有些则不会包含。 某些数据库可能会包含未用于事实数据表或相关维度表的表，而其他数据库则不包含。  
  
## <a name="data-sources-and-partition-storage"></a>数据源和分区存储  
 分区基于数据源中的表或视图，或者基于数据源视图中的表或命名查询。 分区数据的存储位置是由数据源绑定定义的。 通常，可以对度量值组进行水平或垂直分区：  
  
-   在水平分区的度量值组中，其中的每个分区都基于一个单独的表。 此分区类型适用于数据被分隔为多个表的情况。 例如，在某些关系数据库中，对每个月的数据都使用一个单独的表。  
  
-   在垂直分区的度量值组中，度量值组基于单个表，并且每个分区基于筛选该分区数据的源系统查询。 例如，如果一个表中包含几个月的数据，则通过应用 Transact-SQL WHERE 子句以返回每个分区的每个月的数据，仍可以按月份对度量值组进行分区。  
  
 每个分区都有存储设置，用来确定分区的数据和聚合是存储在本地 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中，还是存储在使用其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例的远程分区中。 存储设置还可以指定存储模式，并指定是否使用主动缓存来控制分区的滞后时间。 有关详细信息，请参阅[分区存储模式和处理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)，[主动缓存 &#40;分区 &#41;](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md)，和[远程分区](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)。  
  
## <a name="incremental-updates"></a>增量更新  
 在多分区的度量值组中创建和管理分区时，必须十分谨慎，以确保多维数据集数据的准确性。 虽然对于单分区的度量值组通常不需要特别谨慎，但在对这些分区进行增量更新时则需要十分小心。 对分区进行增量更新时，将创建与源分区具有相同结构的新临时分区。 临时分区在被处理后将与源分区合并。 因此，必须确保填充临时分区的处理查询不会复制现有分区中的任何已有数据。  
  
## <a name="see-also"></a>另请参阅  
 [配置度量值属性](../../analysis-services/multidimensional-models/configure-measure-properties.md)   
 [多维模型中的多维数据集](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
