---
title: DrilldownMemberTop (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3dd1128bfafb052936e742f7ce56529b1222333a
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62690848"
---
# <a name="drilldownmembertop-mdx"></a>DrilldownMemberTop (MDX)


  深化第一个指定集与第二个指定集的交集中的成员，并将结果集的成员数限制为指定数目。 或者，此函数向下钻取上一组通过使用第一个元组层次结构或有选择地指定层次结构的元组。  
  
## <a name="syntax"></a>语法  
  
```  
  
DrillDownMemberTop(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expression>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
 *Count*  
 指定要返回的元组数的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
 *Hierarchy*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *递归*  
 指示集的递归比较的关键字。  
  
 *Include_Calc_Members*  
 用于使计算成员能够包括在深化结果中的关键字。  
  
## <a name="remarks"></a>备注  
 如果指定了数值表达式，则**DrilldownMemberTop**函数排序，计算出的子降序排序，根据数值表达式的值在第一个集中每个成员的子级成员。 如果未指定数值表达式，则此函数根据由查询上下文确定的子成员集所表示的单元值，对第一个集中每个成员的子成员按降序排序。 此行为类似于 TopCount 和 Head (MDX) 函数，都以自然顺序返回一组成员，没有任何排序。  
  
 排序后， **DrilldownMemberTop**函数返回包含父成员的子成员中指定数量的集中*计数，* 具有最高值，且同时包含两个集内.  
  
 如果**递归**函数对第一个集进行排序，如前面所述，然后以递归方式比较的第一个集中，成员按层次结构中，针对第二个集指定 *。* 此函数检索数目的第一个集还存在第二个集中的每个成员的子级的最顶层。  
  
 第一个集可以包含元组，但不能包含成员。 元组的深化是 OLE DB 的扩展，它返回元组集而非成员集。  
  
 **DrilldownMemberTop**函数是类似于[DrilldownMember](../mdx/drilldownmember-mdx.md)函数，但而不是包括也是在第一个集中的每个成员的所有子级将呈现在第二个集中， **DrilldownMemberTop**函数返回最顶层子成员的每个成员数目。  
  
 查询 XMLA 属性 MdpropMdxDrillFunctions，您可以验证的服务器为钻取功能; 提供的支持级别请参阅[支持的 XMLA 属性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)有关详细信息。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
