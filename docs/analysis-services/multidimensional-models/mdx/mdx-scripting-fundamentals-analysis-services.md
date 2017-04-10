---
title: "MDX 脚本编写基础知识 (Analysis Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
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
  - "多维数据集 [Analysis Services], 脚本"
  - "计算 [Analysis Services], 脚本"
  - "MDX [Analysis Services], 脚本"
  - "脚本 [MDX]"
  - "多维数据集 [Analysis Services], 计算"
  - "多维表达式 [Analysis Services], 脚本"
ms.assetid: fdecb3ce-7c87-4bab-8000-532ba7a29f96
caps.latest.revision: 34
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 34
---
# MDX 脚本编写基础知识 (Analysis Services)
  在 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中，多维表达式 (MDX) 脚本由一个或多个 MDX 表达式或语句构成，这些表达式或语句使用计算结果填充多维数据集。  
  
 MDX 脚本定义多维数据集的计算过程。 MDX 脚本也被视为多维数据集的一部分。 因此，更改与多维数据集相关联的 MDX 脚本将会立即更改多维数据集的计算过程。  
  
 要创建 MDX 脚本，您可以使用 [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)]中的“多维数据集设计器”。 有关详细信息，请参阅[定义赋值和其他脚本命令](../../../analysis-services/multidimensional-models/define-assignments-and-other-script-commands.md)和 [Microsoft SQL Server 2005 中的 MDX 脚本简介](http://go.microsoft.com/fwlink/?LinkId=81892)。  
  
 有关与 MDX 查询和计算相关的性能问题，请参阅 [SQL Server Analysis Services 性能指南](http://go.microsoft.com/fwlink/p/?LinkId=399050)的“MDX 优化”部分。  
  
## 本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[基本 MDX 脚本 (MDX)](../../../analysis-services/multidimensional-models/mdx/the-basic-mdx-script-mdx.md)|详细介绍了基本 MDX 脚本（包括每个多维数据集中提供的默认 MDX 脚本），以及 MDX 脚本通常如何在 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中的多维数据集内运行。|  
|[管理作用域和上下文 (MDX)](../../../analysis-services/multidimensional-models/mdx/managing-scope-and-context-mdx.md)|介绍如何使用 [CALCULATE](../Topic/CALCULATE%20Statement%20\(MDX\).md) 语句、 [SCOPE](../Topic/SCOPE%20Statement%20\(MDX\).md) 语句以及 [This](../../../mdx/this-mdx.md) 函数管理 MDX 脚本中的上下文和作用域。|  
|[使用变量和参数 (MDX)](../../../analysis-services/multidimensional-models/mdx/using-variables-and-parameters-mdx.md)|介绍如何在 MDX 脚本中使用变量和参数。|  
|[错误处理 (MDX)](../../../analysis-services/multidimensional-models/mdx/error-handling-mdx.md)|介绍 MDX 脚本中的错误处理。|  
|[支持的 MDX (MDX)](../../../analysis-services/multidimensional-models/mdx/supported-mdx-mdx.md)|提供 MDX 脚本中支持的 MDX 运算符、语句和函数的列表。|  
  
## 另请参阅  
 [MDX 语言参考 (MDX)](../../../mdx/mdx-language-reference-mdx.md)  
  
  