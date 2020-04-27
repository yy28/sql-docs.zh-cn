---
title: 元组 |Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 35b629ae-b1ef-44b1-b556-96956aeb56e7
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5025d76d439933f7392d55661ca52d3f33992db8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2020
ms.locfileid: "66073769"
---
# <a name="tuples"></a>元组
  一个元组唯一标识多维数据集中数据的一个切片。 只要没有两个或多个成员属于相同的层次结构，元组就由维度成员的组合构成。  
  
## <a name="implicit-or-default-attribute-members-in-a-tuple"></a>元组中的隐式或默认属性成员  
 在 MDX 查询或表达式中定义元组时，不必显式包含每个属性层次结构中的属性成员。 如果属性层次结构中的成员未显式包含在查询或表达式中，则该属性层次结构的默认成员为隐式包含在元组中的属性成员。 除非在多维数据集中进行显式定义，否则每个属性层次结构的默认成员均为“(全部)”成员（如果存在“(全部)”成员）。 如果属性层次结构中不存在“(全部)”成员，则默认成员为属性层次结构中的顶级成员。 除非显式定义了默认度量值，否则默认度量值为多维数据集中指定的第一个度量值。 有关详细信息，请参阅[定义默认成员](../attribute-properties-define-a-default-member.md)和 [DefaultMember (MDX)](/sql/mdx/defaultmember-mdx)。  
  
 例如，以下元组通过仅显式定义 Measures 维度的一个成员来标识 Adventure Works 数据库中的一个单元。  
  
```  
(Measures.[Reseller Sales Amount])  
```  
  
 上面的示例唯一标识了由 Measures 维度的 Reseller Sales Amount 成员和多维数据集各属性层次结构的默认成员组成的单元。 默认成员为除 Destination Currency 属性层次结构之外的各个属性层次结构的“(全部)”成员。 Destination Currency 层次结构的默认成员为 US Dollar 成员（此默认成员是在 MDX 脚本中为 Adventure Works 多维数据集定义的）。  
  
 以下查询将返回前面示例指定元组所引用的单元的值 ($80,450.596.98)。  
  
```  
SELECT   
Measures.[Reseller Sales Amount] ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  为查询中的集（此处由单个元组构成）指定轴时，必须在为行轴指定集之前先为列轴指定集。 列轴也可称为“axis(0)”或简称“0”****。 有关 MDX 查询的详细信息，请参阅[基本 MDX 查询 (MDX)](mdx-query-the-basic-query.md)。  
  
### <a name="tuples-as-values-or-member-references"></a>作为值或成员引用的元组  
 如前面的示例所示，您可以在查询中使用元组返回该元组所引用的单元的值。 或者您也可以在表达式中使用元组显式引用该元组中指定的成员。 查询或表达式可使用返回元组或获取元组的函数。 元组可用来引用它所指定的单元的值，或者用来指定成员组合（当元组用在函数中时）。  
  
### <a name="tuple-dimensionality"></a>元组维数  
 元组的 ** “维数”指元组中成员的序列或顺序。 由于隐式成员总是以相同的顺序出现，因此维数通常是针对元组的显式定义成员而言。 定义元组集时，元组成员的顺序非常重要。 以下示例在列轴上的一个元组中包含了两个成员。  
  
```  
SELECT   
([Measures].[Reseller Sales Amount],[Date].[Calendar Year].[CY 2004]) ON COLUMNS   
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  从多个维度显式指定元组中的成员时，必须将整个元组包含在括号中。 如果仅指定元组中的一个成员，则括号是可选的。  
  
 在前面的示例中，查询中的元组指定返回位于 Measures 维度的 Reseller Sales Amount Measure 与 Date 维度中 Calendar Year 属性层次结构的 CY 2004 成员相交处的多维数据集单元。  
  
> [!NOTE]  
>  属性成员可以按成员名称或成员键引用。 在前面的示例中，您可以将对 [CY 2004] 的引用替换为对 &[2004] 的引用。  
  
## <a name="see-also"></a>另请参阅  
 [MDX &#40;Analysis Services 中的关键概念&#41;](../key-concepts-in-mdx-analysis-services.md)   
 [多维数据集空间](cube-space.md)   
 [Autoexists](autoexists.md)   
 [使用成员、元组和集 (MDX)](working-with-members-tuples-and-sets-mdx.md)  
  
  
