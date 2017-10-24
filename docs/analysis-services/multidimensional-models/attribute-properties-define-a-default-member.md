---
title: "定义默认成员 |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default members
- attributes [Analysis Services], default members
- members [Analysis Services], default
- DefaultMember property
ms.assetid: db487856-ee21-49c3-aa08-d9136e193374
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 642c8ceb45d5a756f8fad396d0fb1bf48138afb0
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="attribute-properties---define-a-default-member"></a>特性属性-定义默认成员
  在查询中不包括特性层次结构的情况下，可以使用特性层次结构的默认成员来计算表达式。 如果查询包括的特性层次结构或用户层次结构包含产生特性层次结构的特性，那么将忽略默认成员。 这是因为将使用查询中指定的成员。  
  
 通过将某个特性成员指定为特性层次结构的 **DefaultMember** 属性值，可设置特性层次结构的默认成员。 可以在维度设计器的“维度结构”选项卡上，或在 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]中多维数据集设计器的“计算”选项卡上多维数据集计算脚本中设置该属性。 在定义维度安全性时，还可以在“维度数据”选项卡上指定安全性角色的 **DefaultMember** 属性（覆盖维度的默认成员设置）。 若要避免名称解析问题，可在下列情况下在多维数据集的 MDX 脚本里定义该默认成员：如果多维数据集多次引用某个数据库维度，如果多维数据集内的维度名称与数据库内的维度名称不同，或者如果希望在不同的多维数据集内有不同的默认成员。  
  
 特性的默认成员用于在查询中不包括特性的情况下计算表达式。 特性的默认成员由特性的 **DefaultMember** 属性来指定。 当查询中包括维度的层次结构时，将忽略与该层次结构中的级别相对应的特性中的所有默认成员。 如果查询中不包括维度的层次结构，则默认成员将用于该维度的所有特性中。  
  
## <a name="resolving-the-default-member-when-no-default-member-is-specified"></a>未指定默认成员时解析默认成员  
 如果没有为特性层次结构指定任何默认成员，并且特性层次结构是可聚合的（特性的 **IsAggregatable** 属性设置为 **True**），则“(全部)”成员将作为默认成员。 如果未指定任何默认成员并且特性是不可聚合的（特性的 **IsAggregatable** 属性设置为 **False**），则将从特性层次结构顶层中选择默认成员。  
  
## <a name="specifying-the-default-member"></a>指定默认成员  
 在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 中，维度中的每个特性具有一个默认成员，可以使用特性的 **DefaultMember** 属性指定该成员。 如果属性没有包含在查询中，则使用该设置计算表达式。 如果查询在维度中指定了层次结构，则忽略层次结构中属性的默认成员。 如果查询没有在维度中指定层次结构，则维度属性的 **DefaultMember** 设置便会生效。  
  
 如果特性的 **DefaultMember** 设置为空，并且其 **IsAggregatable** 属性设置为 **True**，则默认成员为“全部”成员。 如果 **IsAggregatable** 属性设置为 **False**，则默认成员为第一个可见级别的第一个成员。  
  
 属性的 **DefaultMember** 设置应用于该属性所参与的每个层次结构。 您不能在一个维度中针对不同的层次结构使用不同的设置。 例如，如果 [1998] 成员是“[年]”属性的默认成员，则该设置应用于维度中的每个层次结构。 在这种情况下， **DefaultMember** 设置不能在一个层次结构中为 [1998]，而在另一个层次结构中为 [1997]。  
  
 如果您为不自然聚合的层次结构中特定级别定义默认成员，则必须定义在层次结构中位于该级别之上的所有级别的默认成员。 例如，在层次结构“全部 - 国家（地区）- 气候”中，您不能定义“气候”的默认成员，除非定义了“国家（地区）”的默认成员。 执行此操作失败会导致查询时错误。  
  
 当层次结构中的各级别自然聚合时，您可以为层次结构中的任意属性定义默认成员，而不考虑该层次结构中的其他属性。 例如，在层次结构“国家（地区）- 省市自治区 - 市县”中，您可以在不定义“省市自治区”或“国家（地区）”的默认成员的情况下为“市县”（例如，[市县].[蒙特利尔]）定义默认成员。  
  
## <a name="see-also"></a>另请参阅  
 [配置属性层次结构的“(全部)”级别](../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  

