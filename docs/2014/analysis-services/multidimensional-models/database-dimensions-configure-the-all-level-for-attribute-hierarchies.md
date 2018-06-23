---
title: 为属性层次结构配置 (All) 级别 |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
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
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: e61b7606ab4a7c2418294133ad7c4f3b03672df1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137629"
---
# <a name="configure-the-all-level-for-attribute-hierarchies"></a>配置属性层次结构的“(全部)”级别
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，“(全部)”级别是一个系统生成的可选级别。 该级别只包含一个成员，该成员的值是直接从属级别中所有成员值的聚合。 该成员称为“全部”成员。 该成员是系统生成的成员，在维度表中不包含该成员。 由于“(全部)”级别中的成员位于层次结构的顶层，因此成员的值是层次结构中所有成员值合并计算的聚合。 “全部”成员通常作为层次结构的默认成员。  
  
 取决于属性层次结构中为 (All) 级别是否存在`IsAggregatable`取决于该属性以及是否存在用户定义的层次结构中为 (All) 级别的属性设置`IsAggregatable`最顶层级别的特性属性用户定义的层次结构。 如果将 `IsAggregatable` 属性设置为 `True`，则会存在“(全部)”级别。 如果将 `IsAggregatable` 属性设置为 `False`，则层次结构中没有“(全部)”级别。  
  
## <a name="establishing-the-topmost-level"></a>建立最顶层级别  
 如果在层次结构中将某级别的源特性的 `IsAggregatable` 属性设置为 `False`，则该级别上面的层次结构中不会出现可聚合级别。 不可聚合的级别必须是任意层次结构的最顶层级别，或者该级别上面的所有级别的源特性的 `IsAggregatable` 属性必须也设置为 `False`。  
  
## <a name="all-member-and-all-level"></a>“全部”成员和“(全部)”级别  
 “(全部)”级别中的单个成员称为“全部”成员。 `AttributeAllMemberName`对维度属性在维度中指定属性的全部成员的名称。 层次结构的 `AllMemberName` 属性指定层次结构的“全部”成员的名称。  
  
## <a name="see-also"></a>请参阅  
 [定义默认成员](attribute-properties-define-a-default-member.md)  
  
  