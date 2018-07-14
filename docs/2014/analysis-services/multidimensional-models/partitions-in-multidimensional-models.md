---
title: 多维模型中的分区 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 26e01dc7-fa49-4b1f-99eb-7799d1b4dcd2
caps.latest.revision: 7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7491322b775cca1a6cf65b667ffd979aa723af0e
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270253"
---
# <a name="partitions-in-multidimensional-models"></a>多维模型中的分区
  在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]中，“分区”  提供加载到度量值组中的事实数据的物理存储。 对于每个度量值组都会自动创建一个分区，但是，常见的情况是创建更多分区以进一步对数据进行分段，从而使处理更高效，查询性能更佳。  
  
 处理更高效是因为分区可以在一个或多个服务器上以并行方式独立处理。 查询运行得更快是因为每个分区都可配置为具有存储模式和聚合优化，从而缩短响应时间。 例如，为包含较新数据的分区选择 MOLAP 存储通常比选择 ROLAP 存储要快。 同样，如果您按日期选择分区，则包含较新数据的分区比包含较旧数据且较少访问的分区可进行更多优化。 请注意，不断变化的存储和按分区的聚合设计对以后的合并操作有不利影响。 在优化各个分区之前，请务必考虑合并操作对于您的分区管理策略而言是否是必要的。  
  
> [!NOTE]  
>  在 Business Intelligence Edition 和 Enterprise Edition 中，提供多分区支持。 Standard Edition 不支持多分区。 有关详细信息，请参阅 [Features Supported by the Editions of SQL Server 2014](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)。  
  
## <a name="important-considerations-when-designing-a-partitioning-strategy"></a>设计分区策略时需要考虑的重要事项  
 多维数据集数据的完整性依赖于数据在多维数据集的分区上的分布情况，要求各个分区上的数据不重复。 从分区汇总数据时，将汇总在多个分区中存在的任何数据元素，就好像它们是不同的数据元素。 这可能导致不正确的汇总和向最终用户提供错误的数据。 例如，如果产品 X 的销售交易在两个分区的事实表中是重复的，汇总产品 X 的销售额可能包含对重复交易的双倍计入。  
  
 分区可以合并；您可以在总体存储和数据更新策略中使用此功能。 仅当分区具有相同的存储模式和聚合设计时，才能合并它们。 为了创建已备以后合并的候选分区，在创建分区时可以复制另一个分区的聚合设计。 在创建分区以复制另一个分区的聚合设计后，还可以编辑该分区。 在进行分区合并时还必须小心，以避免最终分区中的数据重复，这可能导致多维数据集数据不准确。  
  
## <a name="local-partitions"></a>本地分区  
 本地分区是在一个服务器上定义、处理和存储的分区。 如果多维数据集中有大型度量值组，则可能要对其分区，以便可以进行跨分区并行处理。 其优点在于并行处理的执行速度更快。 因为单分区处理作业不必等到一个作业结束之后才能启动另一个作业，所以可以并行运行。 有关详细信息，请参阅[创建和管理本地分区 (Analysis Services)](create-and-manage-a-local-partition-analysis-services.md)。  
  
## <a name="remote-partitions"></a>远程分区  
 远程分区是指在一个服务器上定义，但在其他服务器上处理和存储的分区。 如果要将数据和元数据的存储分布到多个服务器上，则可使用远程分区。 通常，从开发转换到生产时，分析中的数据规模会增大好几倍。 在数据块区如此大的情况下，一个可能的选择就是将该数据分布到多个计算机上。 这不仅是因为数据超过了一台计算机的容量，还因为您可以使用多台计算机来并行处理数据。 有关详细信息，请参阅[创建和管理远程分区&#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)。  
  
## <a name="aggregations"></a>Aggregations  
 聚合是预先计算的多维数据集数据的汇总，可帮助启用 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 以提供快速的查询响应。 您可以通过设置存储限制、性能提升，或在聚合生成进程运行一段时间之后随意停止该进程来控制为度量值组创建的聚合数。 聚合并不一定越多越好。 每增加一个聚合都会带来一定成本，包括硬盘空间和处理时间方面的成本。 我们建议以提升 30% 的性能为标准来创建聚合，然后仅当有测试或体验保证时才增加聚合数量。有关详细信息，请参阅[设计聚合（Analysis Services - 多维）](designing-aggregations-analysis-services-multidimensional.md)。  
  
## <a name="partition-merging-and-editing"></a>分区合并和编辑  
 如果两个分区使用同样的聚合设计，则可以将两个分区合并为一个。 例如，如果有一个按月分区的库存维度，则在每个日历月月末，可以将该月分区与现有的年初至今分区合并。 这样一来，就可对当前月分区进行快速处理和分析，而该年剩下的月只需要在合并时重新处理。 此类重新处理需要较长的处理时间，运行效率也可能较低。 有关管理分区合并过程的详细信息，请参阅[Analysis Services 中合并分区&#40;SSAS-多维&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)。 若要通过编辑多维数据集分区**分区**选项卡中多维数据集设计器，请参阅[编辑或删除分区&#40;Analysis Services-多维&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)。  
  
## <a name="related-topics"></a>相关主题  
  
|主题|Description|  
|-----------|-----------------|  
|[创建和管理本地分区&#40;Analysis Services&#41;](create-and-manage-a-local-partition-analysis-services.md)|包含有关如何使用筛选器或不含重复数据的不同事实表对数据分区的信息。|  
|[设置分区存储&#40;Analysis Services-多维&#41;](set-partition-storage-analysis-services-multidimensional.md)|说明如何为分区配置存储。|  
|[编辑或删除分区&#40;Analysis Services-多维&#41;](edit-or-delete-partitions-analyisis-services-multidimensional.md)|说明如何查看和编辑分区。|  
|[Analysis Services 中合并分区&#40;SSAS-多维&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)|包含有关如何合并分区的信息，这些分区具有不同的事实表或数据切片而不含重复数据。|  
|[设置分区写回](set-partition-writeback.md)|提供有关对分区启用写操作的说明。|  
|[创建和管理远程分区&#40;Analysis Services&#41;](create-and-manage-a-remote-partition-analysis-services.md)|说明如何创建和管理远程分区。|  
  
  
