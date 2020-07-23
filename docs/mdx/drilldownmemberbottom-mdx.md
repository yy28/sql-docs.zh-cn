---
title: DrilldownMemberBottom （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 442f9c57124e06236d50d60f0e5db1de3ebbe731
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86971495"
---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)


  深化第一个指定集与第二个指定集的交集中的成员，并将结果集的成员数限制为指定数目。 此外，此函数还通过使用第一个元组层次结构或选择性指定的层次结构来深化一组元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
DrillDownMemberBottom(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expresion>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
 *计数*  
 指定要返回的元组数的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
 *层次结构*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *Recursive*  
 指示集的递归比较的关键字。  
  
 *Include_Calc_Members*  
 用于使计算成员能够包括在深化结果中的关键字。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则**DrilldownMemberBottom**函数将根据数值表达式的值以升序顺序对第一组中每个成员的子成员进行排序。 如果未指定数值表达式，此函数将根据由查询上下文决定的子成员集所表示的单元的值，对第一个集中每个成员的子成员按升序排序。 此行为类似于 BottomCount 和 Tail (MDX) 函数，都以自然顺序返回一组成员，没有任何排序。  
  
 排序后， **DrilldownMemberBottom**函数将返回一个集，该集包含父成员以及在*Count*中指定的具有最小值的子成员的数量，同时包含这两个集。  
  
 如果指定了**RECURSIVE** ，函数将按前面所述对第一个集进行排序，然后以递归方式将第一个集的成员（如层次结构中的组织）与第二个集进行比较。 此函数检索第一个集与第二个集的交集中每个成员的指定数目的最底层子成员。  
  
 第一个集可以包含元组，但不能包含成员。 元组的深化是 OLE DB 的扩展，它返回元组集而非成员集。  
  
 **DrilldownMemberBottom**函数类似于[DrilldownMember](../mdx/drilldownmember-mdx.md)函数，但对于第一个集中还存在于第二个集中的每个成员， **DrilldownMemberBottom**函数将返回最接近每个成员的子成员数。  
  
 通过查询 XMLA 属性 MdpropMdxDrillFunctions，可以验证服务器为钻取函数提供的支持级别;有关详细信息，请参阅[&#40;xmla&#41;支持的 Xmla 属性](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
