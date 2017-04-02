---
title: "MDX 查询基础知识 (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/13/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "语句 [MDX]"
  - "多维表达式 [Analysis Services], 语句"
  - "多维表达式 [Analysis Services], 查询"
  - "MDX [Analysis Services], 语句"
  - "MDX 查询 [Analysis Services]"
  - "MDX [Analysis Services], 查询"
  - "查询 [MDX]"
ms.assetid: a560383b-bb58-472e-95f5-65d03d8ea08b
caps.latest.revision: 31
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 30
---
# MDX 查询基础知识 (Analysis Services)
  通过使用多维表达式 (MDX)，您可以查询多维对象（如多维数据集）并返回包含多维数据集数据的多维单元集。 本主题及其子主题提供 MDX 查询的概述。  
  
 下列主题介绍了 MDX 查询及其产生的单元集，还提供了有关基本 MDX 语法的详细信息。  
  
> [!NOTE]  
>  有关与 MDX 查询和计算相关的性能问题的详细信息，请参阅 [SQL Server 2005 Analysis Services 性能指南](http://go.microsoft.com/fwlink/?LinkId=81621)中的“编写有效的 MDX”。  
  
## 本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[基本 MDX 查询 (MDX)](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-query-mdx.md)|提供 MDX SELECT 语句的基本语法信息。|  
|[用查询轴和切片器轴限定查询 (MDX)](../Topic/Restricting%20the%20Query%20with%20Query%20and%20Slicer%20Axes%20\(MDX\).md)|说明什么是查询轴和切片器轴，以及如何指定它们。|  
|[在查询中建立多维数据集上下文 (MDX)](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)|介绍 MDX SELECT 语句中的 FROM 子句的用途。|  
|[在 MDX 中生成命名集 (MDX)](../../../analysis-services/multidimensional-models/mdx/building-named-sets-in-mdx-mdx.md)|介绍 MDX 中的命名集的用途，以及在 MDX 查询中创建与使用命名集所需的技术。|  
|[在 MDX 中生成计算成员 (MDX)](../../../analysis-services/multidimensional-models/mdx/building-calculated-members-in-mdx-mdx.md)|提供有关 MDX 中计算成员的信息，包括在 MDX 表达式中创建和使用计算成员所需的技术。|  
|[在 MDX 中生成单元格计算 (MDX)](../../../analysis-services/multidimensional-models/mdx/building-cell-calculations-in-mdx-mdx.md)|详细介绍创建和使用计算单元的过程。|  
|[创建和使用属性值 (MDX)](../Topic/Creating%20and%20Using%20Property%20Values%20\(MDX\).md)|详细介绍创建和使用维度、级别、成员和单元属性的过程。|  
|[操作数据 (MDX)](../../../analysis-services/multidimensional-models/mdx/manipulating-data-mdx.md)|介绍使用钻取和汇总操作数据的基础知识，还介绍了 MDX 中的传递次序和求解次序。|  
|[修改数据 (MDX)](../../../analysis-services/multidimensional-models/mdx/modifying-data-mdx.md)|介绍如何使用写回临时或永久更改多维数据。|  
|[使用变量和参数 (MDX)](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|介绍如何在 MDX 查询中使用变量和参数。|  
  
## 另请参阅  
 [多维表达式 (MDX) 参考](../../../mdx/multidimensional-expressions-mdx-reference.md)  
  
  