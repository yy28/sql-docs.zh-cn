---
title: 维度存储 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: olap
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 88b74cedcff7de22e186f4121fdfb3d5a891f030
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="dimensions---storage"></a>维度的存储
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  维度的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支持两种存储模式：  
  
-   关系 OLAP (ROLAP)  
  
-   多维 OLAP (MOLAP)  
  
 存储模式将确定维度数据的位置和形式。 维度的默认存储模式为 MOLAP。 **相关主题：**[分区存储模式和处理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
## <a name="molap"></a>MOLAP  
 使用 MOLAP 的维度的数据存储在 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 实例中的多维结构中。 该多维结构是在处理维度时创建和填充的。 MOLAP 维度提供的查询性能比 ROLAP 维度更好。  
  
## <a name="rolap"></a>ROLAP  
 使用 ROLAP 的维度的数据实际上存储在用于定义维度的表中。 ROLAP 存储模式无需复制大量数据就可用来支持大型维度，但会降低查询性能。 维度直接依赖于数据源视图中用于定义维度的表，因此 ROLAP 存储模式还可支持实时 OLAP。  
  
> [!IMPORTANT]  
>  如果维度使用 ROLAP 存储模式并且此维度包括在使用 MOLAP 存储的多维数据集中，则对其源表进行架构更改之后，必须立即进行多维数据集处理。 如果执行此操作失败，则可能会导致对多维数据集进行查询时得到不一致的结果。 **相关的主题：**[自动执行 Analysis Services Administrative Tasks with SSIS](../../analysis-services/instances/automate-analysis-services-administrative-tasks-with-ssis.md)。  
  
## <a name="see-also"></a>另请参阅  
 [分区存储模式和处理](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md)  
  
  
