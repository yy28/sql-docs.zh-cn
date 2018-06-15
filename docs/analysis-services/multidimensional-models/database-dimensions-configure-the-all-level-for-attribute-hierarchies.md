---
title: 为属性层次结构配置 (All) 级别 |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 23b00a88c8abf80045a38d0b8cc5d0c695949b0b
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34021674"
---
# <a name="database-dimensions---configure-the-all-level-for-attribute-hierarchies"></a>数据库维度-为属性层次结构配置 (All) 级别
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，“(全部)”级别是一个系统生成的可选级别。 该级别只包含一个成员，该成员的值是直接从属级别中所有成员值的聚合。 该成员称为“全部”成员。 该成员是系统生成的成员，在维度表中不包含该成员。 由于“(全部)”级别中的成员位于层次结构的顶层，因此成员的值是层次结构中所有成员值合并计算的聚合。 “全部”成员通常作为层次结构的默认成员。  
  
 属性层次结构中是否存在“(全部)”级别取决于特性的 **IsAggregatable** 属性设置，用户定义层次结构中是否存在“(全部)”级别取决于用户定义层次结构最顶层级别的特性的 **IsAggregatable** 属性。 如果将 **IsAggregatable** 属性设置为 **True**，则存在“(全部)”级别。 如果将 **IsAggregatable** 属性设置为 **False**，则层次结构中没有“(全部)”级别。  
  
## <a name="establishing-the-topmost-level"></a>建立最顶层级别  
 如果在层次结构中将某级别的源特性的 **IsAggregatable** 属性设置为 **False** ，则该级别上面的层次结构中不会出现可聚合级别。 不可聚合的级别必须是任意层次结构的最顶层级别，或者该级别上面的所有级别的源特性的 **IsAggregatable** 属性必须也设置为 **False**。  
  
## <a name="all-member-and-all-level"></a>“全部”成员和“(全部)”级别  
 “(全部)”级别中的单个成员称为“全部”成员。 维度的 **AttributeAllMemberName**属性指定维度中属性的“全部”成员的名称。 层次结构的 **AllMemberName** 属性指定层次结构的“全部”成员的名称。  
  
## <a name="see-also"></a>另请参阅  
 [定义默认成员](../../analysis-services/multidimensional-models/attribute-properties-define-a-default-member.md)  
  
  
