---
title: "生成 MDX (MDX) 中的计算的成员 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: multidimensional-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- MDX [Analysis Services], calculated members
- calculated members [MDX]
- Multidimensional Expressions [Analysis Services], calculated members
- queries [MDX], calculated members
ms.assetid: 9322e8b8-43e1-4e02-a7d1-e41a586a5bb8
caps.latest.revision: "29"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 03ee94149faf02f0ef99bdde82f4f5847842fd57
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="mdx-calculated-members---building-calculated-members"></a>MDX 计算成员-生成计算的成员
  在多维表达式 (MDX) 中，计算成员是通过以下方式解析的成员：计算 MDX 表达式以返回值。 这种泛泛的定义所包括的范围十分惊人。 由于能在 MDX 查询中构造和使用计算成员，使得人们能够更有力地驾驭多维数据。  
  
 可以在层次结构中的任意位置创建计算成员。 也可以创建不仅依赖于多维数据集中的现有成员、而且依赖于同一 MDX 表达式中定义的其他计算成员的计算成员。  
  
 可以指定让计算成员使用下列上下文之一：  
  
-   **查询作用域** ：若要创建一个计算成员，该计算成员被定义为 MDX 查询的一部分并且其作用域因此被限制在该查询内，请使用 WITH 关键字。 然后，就可以在 MDX SELECT 语句中使用该计算成员。 通过这种方法，更改用 WITH 关键字创建的计算成员时就不会打乱 SELECT 语句。  
  
     有关如何使用 WITH 关键字创建计算成员的详细信息，请参阅[创建查询作用域的计算成员 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-query-scoped-calculated-members.md)。  
  
-   **会话作用域**：若要创建一个计算成员，使其作用域比查询上下文更广（即，其作用域为 MDX 会话的生存期），请使用 CREATE MEMBER 语句。 使用 CREATE MEMBER 语句定义的计算成员可供该会话中的所有 MDX 查询使用。 例如，CREATE MEMBER 语句对于需要在多种查询中大量重用同一个集的客户端应用程序会非常有用。  
  
     有关如何使用 CREATE MEMBER 语句在会话中创建计算成员的详细信息，请参阅[创建会话作用域的计算成员 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-calculated-members-session-scoped-calculated-members.md)。  
  
## <a name="see-also"></a>另请参阅  
 [CREATE MEMBER 语句 (MDX)](../../../mdx/mdx-data-definition-create-member.md)   
 [MDX 函数引用 (MDX)](../../../mdx/mdx-function-reference-mdx.md)   
 [SELECT 语句 &#40;MDX &#41;](../../../mdx/mdx-data-manipulation-select.md)  
  
  
