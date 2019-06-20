---
title: 聚合和聚合设计 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- aggregations [Analysis Services], about aggregations
- storage [Analysis Services], aggregations
- Storage Design Wizard
- data summary [Analysis Services]
- data storage [Analysis Services]
- storing data [Analysis Services], aggregations
- aggregations [Analysis Services]
ms.assetid: 35bd8589-39fa-4e0b-b28f-5a07d70da0a2
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3897c5e41e16af0a8162b63794760aa4d740353d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62727693"
---
# <a name="aggregations-and-aggregation-designs"></a>聚合和聚合设计
  <xref:Microsoft.AnalysisServices.AggregationDesign> 对象定义一组可在多个分区间共享的聚合定义。  
  
 <xref:Microsoft.AnalysisServices.Aggregation> 对象表示某一维度粒度级别上的度量值组数据的汇总。  
  
 简单 <xref:Microsoft.AnalysisServices.Aggregation> 对象由基本信息和维度组成。 基本信息包括聚合的名称、ID、批注和说明。 维度是包含维度的粒度属性列表的 <xref:Microsoft.AnalysisServices.AggregationDimension> 对象的集合。  
  
 聚合是预先计算好的叶单元数据汇总， 它通过在问题提出之前就准备好答案来缩短查询响应时间。 例如，当数据仓库事实数据表包含数十万行时，如果在查询时必须扫描事实数据表中的所有行并计算总和以计算答案，则请求某个特定产品系列每周销售总额的查询需花费很长时间。 但是，如果用于回答此查询的汇总数据已经预先计算好，则几乎可以立即响应。 这种对汇总数据的预先计算在处理过程中进行，是 OLAP 技术快速响应时间的基础。  
  
 多维数据集是 OLAP 技术将汇总数据组织成为多维结构所使用的方式。 维度及其属性层次结构反映了可以向多维数据集提出哪些查询。 聚合按维度所指定的坐标存储在多维结构单元中。 例如，问题“1998 年产品 X 在西北地区的销售额是多少？” 涉及到三个维度（产品、时间和地域）和一个度量值（销售额）。 在多维数据集中指定坐标（产品 X, 1998, 西北）处单元的值就是这个问题的答案，这是一个单一的数值。  
  
 其他问题可能返回多个值。 例如，“1998 年硬件产品按季度按区域的销售额是多少？” 这类查询会从满足所指定条件的坐标处返回很多单元集。 查询返回的单元数目取决于“产品”维度“硬件”级别中的项目数、1998 年的四个季度和“地域”维度中的地区数目。 如果所有的汇总数据都已经预先计算到聚合中，则这种查询的响应时间仅取决于提取指定单元所需的时间。 无需从事实数据表中计算或读取数据。  
  
 虽然对多维数据集中所有可能的聚合进行预先计算可以使所有查询以最短的时间做出响应，但 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 也可以通过其他预先计算好的聚合轻松地计算某些聚合值。 另外，计算所有可能的聚合需要大量的处理时间和存储空间。 因此，应该综合考虑存储要求和预先计算的可能聚合百分比两方面因素，采纳一个折中方案。 如果没有预先计算任何聚合（即 0%），则多维数据集所需要的处理时间和存储空间量达到最低，但由于必须从叶单元检索回答每个查询所需的数据，然后在查询时聚合数据以回答每个查询，因而查询响应时间可能会很长。 例如，为了回答前面提出的问题（“1998 年产品 X 在西北地区的销售额是多少”）而返回单一数值可能需要读取数千行数据，再从每一行提取用于提供“销售额”度量值的列的值，然后再计算总和。 此外，检索该数据所需的时间长度将因具体取决于选定的数据的存储模式的 MOLAP、 HOLAP 或 ROLAP。  
  
## <a name="designing-aggregations"></a>设计聚合  
 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 集成了复杂的算法来选择预先聚合，以便从预先计算的值可以快速计算其他聚合。 例如，如果“时间”层次结构中“月份”级别的聚合已经预先计算好，则某个“季度”级别的计算只要求对三个数字进行汇总，就可以根据需要很快地计算出结果。 这种技术可节省处理时间并降低存储要求，同时对查询响应时间的影响也最小。  
  
 聚合设计向导提供了一些选项，允许在算法中指定存储和百分比约束，从而综合查询响应时间和存储要求两个因素，采纳一个令人满意的折中方案。 但是，聚合设计向导的算法假定所有可能的查询具有相同的概率。 使用基于使用情况的优化向导，您可以通过分析客户端应用程序所提交的查询来针对度量值组调整聚合设计。 通过使用向导来优化多维数据集的聚合，可以使频繁出现的查询迅速地做出响应，而不经常出现的查询则可以以稍慢的速度做出响应，这样就不会对多维数据集所需的存储空间造成较大影响。  
  
 聚合通过使用向导进行设计，但实际上在处理为其设计聚合的分区时才得以计算。 创建聚合后，如果多维数据集的结构发生更改，或者多维数据集源表中的数据有所添加或更改，则通常都需要检查多维数据集的聚合，并重新处理该多维数据集。  
  
## <a name="see-also"></a>请参阅  
 [分区存储模式和处理](partitions-partition-storage-modes-and-processing.md)  
  
  
