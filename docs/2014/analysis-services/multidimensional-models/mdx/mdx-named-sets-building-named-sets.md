---
title: 生成的命名集的 MDX (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], named sets
- named sets [MDX]
- sets [MDX]
- MDX [Analysis Services], named sets
- queries [MDX], named sets
- set expressions [MDX]
ms.assetid: 213b0035-e96d-4ba0-83f2-ded206905603
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b390fd7b731f37be46aae06f0b79473bda4f2e81
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083056"
---
# <a name="building-named-sets-in-mdx-mdx"></a>在 MDX 中生成命名集 (MDX)
  集表达式可能是较长且非常复杂的声明，因此很难理解。 或者，可能非常频繁地使用集表达式，以致于重复定义集成为一种负担。 为了使长而复杂的表达式或常用的表达式更易于使用，多维表达式 (MDX) 允许使用“命名集”表达式。  
  
 从根本上说，命名集就是指定了别名的集表达式。 命名集可包含能正常合并到集中的任何成员或函数。 由于 MDX 将命名集别名视为集表达式，因此您可以在任何能使用集表达式的位置使用命名集别名。  
  
 可以将命名集定义为具有下列上下文之一：  
  
-   **查询作用域** ：若要创建一个命名集，该命名集被定义为 MDX 查询的一部分并且其作用域因此被限制在该查询内，请使用 WITH 关键字。 然后，就可以在 MDX SELECT 语句中使用该命名集。 通过这种方法，更改用 WITH 关键字创建的命名集时就不会打乱 SELECT 语句。  
  
     有关如何使用 WITH 关键字创建命名集的详细信息，请参阅[创建查询作用域的命名集 (MDX)](mdx-named-sets-creating-query-scoped-named-sets.md)。  
  
-   **会话作用域**：若要创建一个命名集，使其作用域比查询上下文更广（即，其作用域为 MDX 会话的生存期），请使用 CREATE SET 语句。 使用 CREATE SET 语句定义的命名集对该会话中的所有 MDX 查询均可用。 例如，CREATE SET 语句对于需要在多种查询中大量重用某个集的客户端应用程序会非常有用。  
  
     有关如何使用 CREATE SET 语句在会话中创建命名集的详细信息，请参阅[创建会话作用域的命名集 (MDX)](mdx-named-sets-creating-session-scoped-named-sets.md)。  
  
## <a name="see-also"></a>请参阅  
 [SELECT 语句&#40;MDX&#41;](/sql/mdx/mdx-data-manipulation-select)   
 [CREATE SET 语句&#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)   
 [MDX 查询基础知识&#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
