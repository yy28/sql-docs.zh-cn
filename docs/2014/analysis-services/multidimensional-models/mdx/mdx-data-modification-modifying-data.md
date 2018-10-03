---
title: 修改数据 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- modifying data [MDX]
- Multidimensional Expressions [Analysis Services], data modifications
- MDX [Analysis Services], data modifications
- data modifications [MDX]
ms.assetid: 363b662c-b839-4971-bbd7-1842f73ce141
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9e83cd72f972107b83bb6efea27d28857053e200
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48177597"
---
# <a name="modifying-data-mdx"></a>修改数据 (MDX)
  除了使用多维表达式 (MDX) 检索和处理维度数据和多维数据集数据以外，还可以使用 MDX 更新或“写回”维度数据和多维数据集数据。 这些更新可以是暂时的，例如对于推测分析或“假设”分析；也可以是永久的，例如当必须基于数据分析进行更改时。  
  
 数据的更新可以发生在维度级别或多维数据集级别：  
  
 **维度写回**  
 可以使用 [ALTER CUBE 语句 (MDX)](/sql/mdx/mdx-data-definition-alter-cube) 语句更改允许写操作的维度的数据，使用 [REFRESH CUBE 语句 (MDX)](/sql/mdx/mdx-data-definition-refresh-cube) 反映属性值的删除、创建和更新。 还可以使用 ALTER CUBE 语句执行复杂的操作，如删除层次结构中的整个子树以及提升已删除成员的子级。  
  
 **多维数据集写回**  
 可以使用 [UPDATE CUBE](/sql/mdx/mdx-data-manipulation-update-cube) 语句更新启用写操作的多维数据集。 UPDATE CUBE 语句允许您用特定的值更新元组。 可以通过 [REFRESH CUBE 语句 (MDX)](/sql/mdx/mdx-data-definition-refresh-cube) 用来自服务器的更新数据刷新客户端会话中的数据。  
  
 有关详细信息，请参阅[使用多维数据集写回 (MDX)](mdx-data-modification-using-cube-writebacks.md)。  
  
## <a name="see-also"></a>请参阅  
 [MDX 查询基础知识&#40;Analysis Services&#41;](mdx-query-fundamentals-analysis-services.md)  
  
  
