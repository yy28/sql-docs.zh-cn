---
title: 父-子层次结构中的属性 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- data members [Analysis Services]
- nonleaf members
- MembersWithDataCaption property
- members [Analysis Services]
- members [Analysis Services], data
- leaf members
- parent-child dimensions [Analysis Services]
- MembersWithData property
ms.assetid: 249971cc-4bcd-44f1-8241-bdacc04d3d38
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 500740207ea4c020ef7845b5de9e993655d4295d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219647"
---
# <a name="attributes-in-parent-child-hierarchies"></a>父子层次结构中的属性
  在 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]中，通常会对维度中成员的内容做出常规假设。 叶成员包含直接派生自基础数据源的数据；非叶成员包含派生自对子成员所执行的聚合的数据。  
  
 但是在父子层次结构中，一些非叶成员除包含通过子成员聚合的数据外，还可能包含派生自基础数据源的数据。 对于父子层次结构中的这些非叶成员，可创建包含基础事实数据表数据的系统生成的特殊子成员。 这些成员称为“数据成员 ”，它们包含与非叶成员直接相关的值，而非叶成员独立于通过该非叶成员的后代计算的汇总值。  
  
 数据成员仅可用于具有父子层次结构的维度，并且仅当父属性允许时才可见。 可以使用维度设计器来控制数据成员的可见性。 若要公开数据成员，请设置`MembersWithData`到该父特性属性`NonLeafDataVisible.`若要隐藏父特性所包含的数据成员，请设置`MembersWithData`为父特性属性`NonLeafDataHidden`。  
  
 此设置不会覆盖非叶成员的正常聚合行为；为了进行聚合，将始终包括作为子成员的数据成员。 但是，可以用自定义汇总公式来覆盖正常聚合行为。 多维表达式 (MDX) [DataMember](/sql/mdx/datamember-mdx)函数使您能够访问相关的数据成员而不考虑的值的值`MembersWithData`属性。  
  
 `MembersWithDataCaption`父属性的属性提供[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]用于生成数据成员的成员名称的命名模板。  
  
## <a name="using-data-members"></a>使用数据成员  
 根据有父子层次结构的组织维度聚合度量值时，数据成员将非常有用。 例如，以下关系图显示了有三个级别的维度，用于表示产品的总销售量。 第一个级别显示所有销售人员的总销售量。 第二个级别包括按销售经理分组的全体销售职员的总销售量，第三个级别包括按销售人员分组的全体销售职员的总销售量。  
  
 ![具有三个级别的总销售量维度](../media/agdatamember1.gif "具有三个级别的总销售量维度")  
  
 通常，销售经理 1 成员的值派生自 Salesperson 1 和 Salesperson 2 成员的聚合值。 但是，因为销售经理 1 也可销售产品，所以该成员也可能包含从事实数据表派生的数据，原因是其中可能存在与销售经理 1 相关的总销售额。  
  
 此外，每个销售职员成员的个人佣金可能不同。 在这种情况下，与其下属销售人员所产生的总销售额的合计相对比，将使用两种不同的计数法来计算销售经理的个人总销售额的佣金。 因此，能够访问非叶成员的基础事实数据表数据非常重要。 MDX`DataMember`函数可用于检索个人的销售经理 1 成员的总销售量和自定义汇总表达式可用来从提供总的销售经理 1 成员的聚合值中排除数据成员与该成员相关的销售人员的销售额。  
  
## <a name="see-also"></a>请参阅  
 [维度特性属性参考](dimension-attribute-properties-reference.md)   
 [父-子层次结构](parent-child-dimension.md)  
  
  
