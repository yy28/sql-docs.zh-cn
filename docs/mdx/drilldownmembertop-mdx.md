---
title: DrilldownMemberTop （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 5bed7dfcf82b7f768ba1dc1e98128424665af6bd
ms.sourcegitcommit: 205de8fa4845c491914902432791bddf11002945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/23/2020
ms.locfileid: "86970038"
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)


  深化第一个指定集与第二个指定集的交集中的成员，并将结果集的成员数限制为指定数目。 此外，此函数通过使用第一个元组层次结构或选择性指定的层次结构来深化一组元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
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
 如果指定了数值表达式，则**DrilldownMemberTop**函数将根据数值表达式的值以降序顺序对第一个集中每个成员的子成员进行排序。 如果未指定数值表达式，则此函数根据由查询上下文确定的子成员集所表示的单元值，对第一个集中每个成员的子成员按降序排序。 此行为类似于 TopCount 和 Head (MDX) 函数，都以自然顺序返回一组成员，没有任何排序。  
  
 排序后， **DrilldownMemberTop**函数将返回一个集，该集包含父成员以及在*Count*中指定的具有最高值的子成员的数目，并包含在这两个集中。  
  
 如果指定了**RECURSIVE** ，函数将按前面所述对第一个集进行排序，然后以递归方式将第一个集的成员（如层次结构中的组织）与第二个集进行比较。 函数检索第一个集中还存在于第二个集中的每个成员的最顶层子成员数。  
  
 第一个集可以包含元组，但不能包含成员。 元组的深化是 OLE DB 的扩展，它返回元组集而非成员集。  
  
 **DrilldownMemberTop**函数类似于[DrilldownMember](../mdx/drilldownmember-mdx.md)函数，但对于第一个集中还存在于第二个集中的每个成员， **DrilldownMemberTop**函数将返回每个成员的最顶层子成员数。  
  
 通过查询 XMLA 属性 MdpropMdxDrillFunctions，可以验证服务器为钻取函数提供的支持级别;有关详细信息，请参阅[&#40;xmla&#41;支持的 Xmla 属性](https://docs.microsoft.com/analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)。  
  
## <a name="example"></a>示例  
 下例深化了服装类别，返回已发货订单数量最多的三个服装子类别。  
  
```  
SELECT DrilldownMemberTop   ({[Product].[Product Categories].[All Products],        
[Product].[Product Categories].[Category].Bikes,        
[Product].[Product Categories].[Category].Clothing},     
{[Product].[Product Categories].[Category].Clothing},     
3,     
[Measures].[Reseller Order Quantity])     
ON 0     
FROM [Adventure Works]     
WHERE [Measures].[Reseller Order Quantity]  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
