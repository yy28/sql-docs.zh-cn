---
title: 多维数据集存储（Analysis Services 多维数据） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- measure groups [Analysis Services], cubes
- cubes [Analysis Services], storage
- linked measure groups [Analysis Services]
- storing data [Analysis Services], cubes
- partitions [Analysis Services], cubes
- storage [Analysis Services], cubes
ms.assetid: 1b1ad360-9a9b-4996-bee9-84238a2bb4ac
author: minewiskan
ms.author: owend
ms.openlocfilehash: eef1dd188b0038c637dc15750a6538c929359299
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84545273"
---
# <a name="cube-storage-analysis-services---multidimensional-data"></a>多维数据集存储（Analysis Services - 多维数据）
  存储可能仅包括多维数据集元数据，也可能包括事实数据表中的所有源数据以及通过与度量值组相关的维度所定义的聚合。 存储的数据数量取决于所选择的存储模式和聚合数。 存储的数据的量会直接影响查询性能。 [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 使用几种方法来最大程度地减少存储多维数据集数据和聚合所需的空间：  
  
-   使用存储选项，您可以选择最适合于多维数据集数据的存储模式和位置。  
  
-   通过一个复杂的算法设计有效的汇总聚合，在不牺牲速度的前提下将存储要求降至最低。  
  
-   不为空单元分配存储空间。  
  
 存储按分区进行定义，并且对于多维数据集中的每个度量值组，至少存在一个分区。 有关详细信息，请参阅[分区 &#40;Analysis Services 多维数据&#41;](partitions-analysis-services-multidimensional-data.md)、[分区存储模式和处理](partitions-partition-storage-modes-and-processing.md)、[度量值和度量值组](../multidimensional-models/measures-and-measure-groups.md)，以及[在多维模型中创建度量值和度量值组](../multidimensional-models/create-measures-and-measure-groups-in-multidimensional-models.md)。  
  
## <a name="partition-storage"></a>分区存储  
 度量值组的存储空间可以分成多个分区。 使用分区，您可以将度量值组分散到单个服务器或多个服务器上的离散段中，并优化存储和查询性能。 度量值组中的每个分区都可基于不同的数据源，并使用不同的存储设置进行存储。  
  
 您可以在创建分区时为分区指定数据源。 还可以更改任何现有分区的数据源。 度量值组可以进行垂直分区，也可以进行水平分区。 垂直分区的度量值组中的每个分区都基于单个源表的筛选视图。 例如，如果度量值组所基于的表包含若干年的数据，则可以为每年的数据创建单独的分区。 相反，水平分区的度量值组中的每个分区都基于单独的表。 如果数据源使用单独的表存储每年的数据，则可以使用水平分区。  
  
 分区最初使用其所属度量值组的存储设置进行创建。 存储设置确定是将详细信息和聚合数据以多维格式存储在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中，还是以关系格式存储在源服务器上，或者是两者的组合。 存储设置还确定是否使用主动缓存来自动处理对存储在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中的多维数据所进行的源数据更改。  
  
 用户看不到多维数据集的分区。 但是，为不同分区选择的存储设置可能影响到数据的即时性、所用磁盘空间的数量和查询性能。 分区可以存储在多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中。 这为多维数据集存储提供了群集途径，并将工作负荷分散到多个 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 服务器上。 有关详细信息，请参阅[分区存储模式和处理](partitions-partition-storage-modes-and-processing.md)、[远程分区](partitions-remote-partitions.md)和[分区 &#40;Analysis Services 多维数据&#41;](partitions-analysis-services-multidimensional-data.md)。  
  
## <a name="linked-measure-groups"></a>链接度量值组  
 在不同 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例上存储多个多维数据集副本可能需要相当大的磁盘空间，但可以通过用链接度量值组替换度量值组副本来大大减少所需空间。 链接度量值组基于其他 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 数据库（位于相同或不同 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中）的多维数据集中的度量值组。 链接度量值组还只能与来自同一源多维数据集的链接维度一起使用。 链接维度和度量值组都使用源多维数据集的聚合，并且对它们自己的聚合没有数据存储要求。 因此，通过在一个数据库中维护源度量值组和维度，而在其他数据库的多维数据集中创建链接多维数据集和维度，您可以因存储所用空间的大大降低而节约大量磁盘空间。 有关详细信息，请参阅[链接度量值组](../multidimensional-models/linked-measure-groups.md)。  
  
## <a name="see-also"></a>另请参阅  
 [聚合和聚合设计](aggregations-and-aggregation-designs.md)  
  
  
