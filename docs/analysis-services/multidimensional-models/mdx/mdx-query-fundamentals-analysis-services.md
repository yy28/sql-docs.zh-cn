---
title: "MDX 查询基础知识 (Analysis Services) |Microsoft 文档"
ms.custom: 
ms.date: 03/13/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- statements [MDX]
- Multidimensional Expressions [Analysis Services], statements
- Multidimensional Expressions [Analysis Services], queries
- MDX [Analysis Services], statements
- MDX queries [Analysis Services]
- MDX [Analysis Services], queries
- queries [MDX]
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 601c9d365870528a8716091cfc3a1ba60bd2f920
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-query-fundamentals-analysis-services"></a>MDX 查询基础知识 (Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]多维表达式 (MDX) 允许你查询多维对象，例如多维数据集，并返回包含多维数据集的数据的多维单元集。 本主题及其子主题提供 MDX 查询的概述。  
  
 下列主题介绍了 MDX 查询及其产生的单元集，还提供了有关基本 MDX 语法的详细信息。  
  
> [!NOTE]  
>  有关与 MDX 查询和计算相关的性能问题的详细信息，请参阅 [SQL Server 2005 Analysis Services 性能指南](http://go.microsoft.com/fwlink/?LinkId=81621)中的“编写有效的 MDX”。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[基本 MDX 查询 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-query-the-basic-query.md)|提供 MDX SELECT 语句的基本语法信息。|  
|[限制查询中的使用查询和切片器轴 &#40;MDX &#41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-and-slicer-axes-restricting-the-query.md)|说明什么是查询轴和切片器轴，以及如何指定它们。|  
|[在查询中建立多维数据集上下文 (MDX)](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|介绍 MDX SELECT 语句中的 FROM 子句的用途。|  
|[在 MDX 中生成命名集 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-named-sets-building-named-sets.md)|介绍 MDX 中的命名集的用途，以及在 MDX 查询中创建与使用命名集所需的技术。|  
|[在 MDX 中生成计算成员 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-building-calculated-members.md)|提供有关 MDX 中计算成员的信息，包括在 MDX 表达式中创建和使用计算成员所需的技术。|  
|[在 MDX 中生成单元格计算 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-cell-calculations-build-cell-calculations.md)|详细介绍创建和使用计算单元的过程。|  
|[创建和使用属性值 (MDX)](http://msdn.microsoft.com/library/0cafb269-03c8-4183-b6e9-220f071e4ef2)|详细介绍创建和使用维度、级别、成员和单元属性的过程。|  
|[操作数据 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)|介绍使用钻取和汇总操作数据的基础知识，还介绍了 MDX 中的传递次序和求解次序。|  
|[修改数据 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-modifying-data.md)|介绍如何使用写回临时或永久更改多维数据。|  
|[使用变量和参数 (MDX)](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|介绍如何在 MDX 查询中使用变量和参数。|  
  
## <a name="see-also"></a>另请参阅  
 [多维表达式 (MDX) 参考](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  
