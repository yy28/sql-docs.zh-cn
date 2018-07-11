---
title: 构建在 MDX (MDX) 中的单元格计算 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- calculated cells [MDX]
- queries [MDX], cell calculations
- cells [MDX]
- MDX [Analysis Services], calculations
- calculation subcubes [MDX]
- calculated values [MDX]
- Multidimensional Expressions [Analysis Services], cell calculations
ms.assetid: 068aea63-d419-4791-a960-3d74e76f808e
caps.latest.revision: 30
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9b0a689858d4012f360e7f3893cfa844f3ecbdcf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161348"
---
# <a name="building-cell-calculations-in-mdx-mdx"></a>在 MDX 中生成单元计算 (MDX)
  多维表达式 (MDX) 提供许多用于生成计算值（如计算成员、自定义汇总以及自定义成员）的工具。 然而，使用这些功能很难影响一组特定的单元或单个单元。  
  
 若要生成专门用于单元的计算值，需要使用 MDX 中的计算单元功能。 计算单元允许您定义单元的特定部分（称为“计算子多维数据集” ），并根据可应用于每个单元的可选条件将某个公式应用于该计算子多维数据集内的各个单元。  
  
 计算单元还提供了复杂的功能，如目标查找公式（如 KPI 中所使用的）或推测分析公式。 此级别的功能来自 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 中的传递次序功能，传递次序功能允许对计算单元进行递归传递，并对传递次序中的特定传递应用计算公式。 有关传递次序的详细信息，请参阅[理解传递次序和求解次序 (MDX)](mdx-data-manipulation-understanding-pass-order-and-solve-order.md)。  
  
 就创建作用域而言，计算单元类似于命名集和计算成员，因为可以为会话或单个查询的生存期临时创建计算单元，或将计算单元作为多维数据集的一部分在全局作用域内使用：  
  
-   **查询作用域：** 若要创建定义为 MDX 查询的一部分的计算单元（计算单元的作用域因此局限于该查询），请使用 WITH 关键字。 然后可以在 MDX SELECT 语句中使用该计算单元。 使用此方法，通过使用创建的计算的单元`WITH`关键字可以更改不会打乱 SELECT 语句。  
  
     有关如何使用 WITH 关键字创建计算成员的详细信息，请参阅[创建查询作用域的单元计算 (MDX)](../../multidimensional-models-olap-logical-cube-objects/calculations.md)。  
  
-   **会话作用域：** 若要创建作用域比查询的上下文更广（也就是说，其作用域是 MDX 会话的生存期）的计算成员，请使用 CREATE CELL CALCULATION 或 ALTER CUBE 语句。  
  
     有关如何使用 CREATE CELL CALCULATION 或 ALTER CUBE 语句在会话中创建计算单元的详细信息，请参阅 [创建会话作用域的计算单元](mdx-cell-calculations-session-scoped-calculated-cells.md)  
  
## <a name="see-also"></a>请参阅  
 [ALTER CUBE 语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-alter-cube)   
 [CREATE CELL CALCULATION 语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-cell-calculation)   
 [创建查询作用域的单元计算&#40;MDX&#41;](../../multidimensional-models-olap-logical-cube-objects/calculations.md)   
 [MDX 查询基础知识&#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
