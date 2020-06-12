---
title: 配置属性层次结构的 "（全部）" 级别 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- All members
- IsAggregatable property
- topmost levels [Analysis Services]
- (All) levels
- AttributeAllMemberName property
- levels [Analysis Services]
- members [Analysis Services], All
- AllMemberName property
ms.assetid: 0cb35e6f-b10f-483d-b893-78f6ca3979fd
author: minewiskan
ms.author: owend
ms.openlocfilehash: 9874a8c8a6861bc7d9e44271b089e8af3a4c0ae2
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84547167"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>配置属性层次结构的“(全部)”级别
  在中 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ，"（全部）" 级别是一个系统生成的可选级别。 该级别只包含一个成员，该成员的值是直接从属级别中所有成员值的聚合。 该成员称为“全部”成员。 该成员是系统生成的成员，在维度表中不包含该成员。 由于“(全部)”级别中的成员位于层次结构的顶层，因此成员的值是层次结构中所有成员值合并计算的聚合。 “全部”成员通常作为层次结构的默认成员。  
  
 属性层次结构中是否存在“(全部)”级别取决于特性的 `IsAggregatable` 属性设置，用户定义层次结构中是否存在“(全部)”级别取决于用户定义层次结构最顶层级别的特性的 `IsAggregatable` 属性。 如果将 `IsAggregatable` 属性设置为 `True`，则会存在“(全部)”级别。 如果将 `IsAggregatable` 属性设置为 `False`，则层次结构中没有“(全部)”级别。  
  
## <a name="establishing-the-topmost-level"></a>建立最顶层级别  
 如果在层次结构中将某级别的源特性的 `IsAggregatable` 属性设置为 `False`，则该级别上面的层次结构中不会出现可聚合级别。 不可聚合的级别必须是任意层次结构的最顶层级别，或者该级别上面的所有级别的源特性的 `IsAggregatable` 属性必须也设置为 `False`。  
  
## <a name="all-member-and-all-level"></a>“全部”成员和“(全部)”级别  
 “(全部)”级别中的单个成员称为“全部”成员。 `AttributeAllMemberName`维度的属性指定维度中属性的 "全部" 成员的名称。 层次结构的 `AllMemberName` 属性指定层次结构的“全部”成员的名称。  
  
## <a name="see-also"></a>另请参阅  
 [定义默认成员](attribute-properties-define-a-default-member.md)  
  
  
