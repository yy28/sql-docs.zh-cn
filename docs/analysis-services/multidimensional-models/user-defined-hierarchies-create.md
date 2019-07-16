---
title: 创建用户定义的层次结构 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f6ca49e3a7714134d554538ae4f37e267999f2c2
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208414"
---
# <a name="user-defined-hierarchies---create"></a>用户定义的层次结构 - 创建
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 可以创建用户定义的层次结构。 层次结构是基于属性的级别集合。 例如，时间层次结构可能包含年、季、月、周和日级别。 在某些层次结构中，每个成员属性唯一对应于它上面的成员属性。 这有时也称为自然层次结构。 最终用户可使用层次结构来浏览多维数据集数据。 在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中，可使用维度设计器的“层次结构”窗格定义层次结构。  
  
 创建用户定义的层次结构时，该层次结构可能是 *不规则*的。 在不规则层次结构中，至少一个成员的逻辑父成员不在该成员的直接上一级中。 层次结构不规则时，可使用一些设置控制缺少的成员是否可见以及如何显示这些缺少的成员。 有关详细信息，请参阅 [不规则层次结构](../../analysis-services/multidimensional-models/user-defined-hierarchies-ragged-hierarchies.md)。  
  
  
## <a name="see-also"></a>请参阅  
 [用户层次结构属性](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-properties.md)   
 [级别属性 - 用户层次结构](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/user-hierarchies-level-properties.md)   
 [父子维度](../../analysis-services/multidimensional-models/parent-child-dimension.md)  
  
  
