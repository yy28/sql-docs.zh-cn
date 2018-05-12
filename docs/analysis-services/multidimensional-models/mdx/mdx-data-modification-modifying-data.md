---
title: 修改数据 (MDX) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f4fdaf60309d09a706fea552722017756b7945d6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-data-modification---modifying-data"></a>MDX 数据修改的修改数据
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  除了使用多维表达式 (MDX) 检索和处理维度数据和多维数据集数据以外，还可以使用 MDX 更新或“写回”维度数据和多维数据集数据。 这些更新可以是暂时的，例如对于推测分析或“假设”分析；也可以是永久的，例如当必须基于数据分析进行更改时。  
  
 数据的更新可以发生在维度级别或多维数据集级别：  
  
 **维度写回**  
 可以使用 [ALTER CUBE 语句 (MDX)](../../../mdx/mdx-data-definition-alter-cube.md) 语句更改允许写操作的维度的数据，使用 [REFRESH CUBE 语句 (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) 反映属性值的删除、创建和更新。 还可以使用 ALTER CUBE 语句执行复杂的操作，如删除层次结构中的整个子树以及提升已删除成员的子级。  
  
 **多维数据集写回**  
 可以使用 [UPDATE CUBE](../../../mdx/mdx-data-manipulation-update-cube.md) 语句更新启用写操作的多维数据集。 UPDATE CUBE 语句允许您用特定的值更新元组。 可以通过 [REFRESH CUBE 语句 (MDX)](../../../mdx/mdx-data-definition-refresh-cube.md) 用来自服务器的更新数据刷新客户端会话中的数据。  
  
 有关详细信息，请参阅[使用多维数据集写回 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-data-modification-using-cube-writebacks.md)。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 查询基础知识 & #40;Analysis Services & #41;](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)  
  
  
