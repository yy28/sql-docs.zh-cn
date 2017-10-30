---
title: "DrilldownMemberBottom (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DRILLDOWNMEMBERBOTTOM
dev_langs:
- kbMDX
helpviewer_keywords:
- DrilldownMemberBottom function
ms.assetid: 603927ba-68f6-4e7a-b17f-44cad33bdfb0
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: d66f9aeb97a5219f85a33acfedb710f980b63401
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="drilldownmemberbottom-mdx"></a>DrilldownMemberBottom (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  深化第一个指定集与第二个指定集的交集中的成员，并将结果集的成员数限制为指定数目。 或者，此函数还向下钻取一组元组上通过使用第一个元组层次结构或 （可选） 指定层次结构。  
  
## <a name="syntax"></a>語法  
  
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
  
 *层次结构*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *递归*  
 指示集的递归比较的关键字。  
  
 *Include_Calc_Members*  
 用于使计算成员能够包括在深化结果中的关键字。  
  
## <a name="remarks"></a>注释  
 如果指定数值表达式，则**DrilldownMemberBottom**函数以升序排序，在第一个组中，根据的数值表达式的值的每个成员的子级，如对子成员组成的集求值排序。 如果未指定数值表达式，此函数将根据由查询上下文决定的子成员集所表示的单元的值，对第一个集中每个成员的子成员按升序排序。 此行为类似于 BottomCount 和 Tail (MDX) 函数，都以自然顺序返回一组成员，没有任何排序。  
  
 排序之后, **DrilldownMemberBottom**函数返回一组包含父成员和中指定的子成员数*计数，*具有最低值和是否包含由两个组。  
  
 如果**递归**指定，则函数进行排序的第一组，如前面所述，然后以递归方式对的第一组的成员进行比较，如在层次结构中，针对第二组中组织。 此函数检索第一个集与第二个集的交集中每个成员的指定数目的最底层子成员。  
  
 第一个集可以包含元组，但不能包含成员。 元组的深化是 OLE DB 的扩展，它返回元组集而非成员集。  
  
 **DrilldownMemberBottom**函数是类似于[DrilldownMember](../mdx/drilldownmember-mdx.md)起作用，但而不是第一组，也是包括每个成员的所有子级显示在第二组**DrilldownMemberBottom**函数返回的最底端每个成员的子成员数目。  
  
 查询的 XMLA 属性 MdpropMdxDrillFunctions，您可以验证服务器提供钻函数; 支持的级别请参阅[支持 XMLA 属性 &#40;XMLA &#41;](../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)有关详细信息。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

