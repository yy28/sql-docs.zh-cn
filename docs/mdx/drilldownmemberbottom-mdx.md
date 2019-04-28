---
title: DrilldownMemberBottom (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 854f880cf9cb4f06ee4fc44fd18cec5f0ab99ca8
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62691067"
---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)


  深化第一个指定集与第二个指定集的交集中的成员，并将结果集的成员数限制为指定数目。 或者，此函数也向下钻取一组元组上通过使用第一个元组层次结构或有选择地指定层次结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
DrillDownMemberBottom(<Set_Expression1>, <Set_Expression2>, <Count> [,[<Numeric_Expresion>] [,[<Hierarchy>]] [,[RECURSIVE][,INCLUDE_CALC_MEMBERS]]])  
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
 如果指定了数值表达式，则**DrilldownMemberBottom**函数排序，按升序排列，根据数值表达式的值在第一个集中每个成员的子级求得的子组成员。 如果未指定数值表达式，此函数将根据由查询上下文决定的子成员集所表示的单元的值，对第一个集中每个成员的子成员按升序排序。 此行为类似于 BottomCount 和 Tail (MDX) 函数，都以自然顺序返回一组成员，没有任何排序。  
  
 排序后， **DrilldownMemberBottom**函数返回包含父成员的子成员中指定数量的集中*计数，* 具有最小值，且同时包含两者设置。  
  
 如果**递归**指定，则该函数对第一个集进行排序，如前面所述，然后以递归方式比较的第一组的成员按层次结构中，针对第二个集。 此函数检索第一个集与第二个集的交集中每个成员的指定数目的最底层子成员。  
  
 第一个集可以包含元组，但不能包含成员。 元组的深化是 OLE DB 的扩展，它返回元组集而非成员集。  
  
 **DrilldownMemberBottom**函数是类似于[DrilldownMember](../mdx/drilldownmember-mdx.md)函数，但而不是包括也是在第一个集中的每个成员的所有子级将呈现在第二个集中， **DrilldownMemberBottom**函数返回的指定数目的每个成员的子成员。  
  
 查询 XMLA 属性 MdpropMdxDrillFunctions，您可以验证的服务器为钻取功能; 提供的支持级别请参阅[支持的 XMLA 属性&#40;XMLA&#41; ](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties)有关详细信息。  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
