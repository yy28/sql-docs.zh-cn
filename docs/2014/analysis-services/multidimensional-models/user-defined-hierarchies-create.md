---
title: 创建用户定义的层次结构 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- user-defined hierarchies [Analysis Services]
ms.assetid: 16715b85-0630-4a8e-99b0-c0d213cade26
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 1a1106c4b374b34351e3375adae102686f7e41fe
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/23/2019
ms.locfileid: "66072568"
---
# <a name="create-user-defined-hierarchies"></a>创建用户定义层次结构
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以创建用户定义的层次结构。 层次结构是基于属性的级别集合。 例如，时间层次结构可能包含年、季、月、周和日级别。 在某些层次结构中，每个成员属性唯一对应于它上面的成员属性。 这有时也称为自然层次结构。 最终用户可使用层次结构来浏览多维数据集数据。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，可使用维度设计器的“层次结构”窗格定义层次结构。  
  
 创建用户定义的层次结构时，该层次结构可能是 *不规则*的。 在不规则层次结构中，至少一个成员的逻辑父成员不在该成员的直接上一级中。 层次结构不规则时，可使用一些设置控制缺少的成员是否可见以及如何显示这些缺少的成员。 有关详细信息，请参阅 [不规则层次结构](user-defined-hierarchies-ragged-hierarchies.md)。  
  
> [!NOTE]  
>  有关与设计和配置用户定义的层次结构相关的性能问题的详细信息，请参阅 [SQL Server 2005 Analysis Services 性能指南](https://docsbay.net/Microsoft-SQL-Server-2005-Analysis-Services-Performance-Guide)。  
  
## <a name="see-also"></a>请参阅  
 [用户层次结构属性](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [级别属性&#91;Paved Over&#93;](../multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [父-子层次结构](parent-child-dimension.md)  
  
  
