---
title: "维度存储 |Microsoft 文档"
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
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- dimensions [Analysis Services], storage
- storing data [Analysis Services]
- storage [Analysis Services], dimensions
- relational OLAP
- multidimensional OLAP
- MOLAP
- storing data [Analysis Services], dimensions
- ROLAP
ms.assetid: 8d74b932-2174-4e1f-8414-636455880b6a
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b70bdcc3883148035437a5097c170cb52536b8e8
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="dimensions---storage"></a>维度的存储
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]维度的[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]支持两种存储模式：  
  
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
  
  
