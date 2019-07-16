---
title: Count （集） (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aac2f72cc8cd91e1964fd7734b858be8215cfdd8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68047291"
---
# <a name="count-set-mdx"></a>Count（集）(MDX)


  返回集中的单元数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Standard syntax  
Count(Set_Expression [ , ( EXCLUDEEMPTY | INCLUDEEMPTY ) ] )  
  
Alternate syntax  
Set_Expression.Count  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 **Count （集）** 函数包括还是排除空单元格，具体取决于所使用的语法。 如果使用标准语法时，可以排除或者通过使用包含空单元格**EXCLUDEEMPTY**或**INCLUDEEMPTY**标记，分别。 如果使用备用语法，则函数始终包括空单元。  
  
 若要排除的一组计数中的空单元，请使用标准语法和可选**EXCLUDEEMPTY**标志。  
  
> [!NOTE]  
>  **Count （集）** 函数对空单元格默认情况下进行计数。 与此相反，**计数**OLE DB，用于计算一组中的函数默认情况下排除空单元格。  
  
## <a name="examples"></a>示例  
 下例统计成员集中单元的数目，该成员集由“产品”维度中“型号名称”属性层次结构的子级构成。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例通过使用计算的 Product 维度中的产品数量**DrilldownLevel**函数结合**计数**函数。  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 下面的示例返回通过使用到上一日历季度相比销售额有所下降的分销商**计数**函数结合**筛选器**函数和许多其他函数。 此查询使用**聚合**函数即可选择多个地域成员，例如对客户端应用程序中的下拉列表中进行选择。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
   (Filter  
      (Existing(Reseller.Reseller.Reseller),  
         [Measures].[Reseller Sales Amount]   
         < ([Measures].[Reseller Sales Amount],  
            [Date].Calendar.PrevMember)  
      )  
   )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate  
   ( {[Geography].[State-Province].&[WA]&[US],   
      [Geography].[State-Province].&[OR]&[US] }   
   )  
SELECT NON EMPTY HIERARCHIZE   
   (AddCalculatedMembers   
      ({DrillDownLevel  
         ({[Product].[All Products]})  
      })  
   ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE ([Geography].[State-Province].x,  
   [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
   ,[Measures].[Declining Reseller Sales])  
  
```  
  
## <a name="see-also"></a>请参阅  
 [计数&#40;维度&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [计数&#40;层次结构级别&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [计数&#40;元组&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel (MDX)](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers (MDX)](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize (MDX)](../mdx/hierarchize-mdx.md)   
 [属性 (MDX)](../mdx/properties-mdx.md)   
 [Aggregate (MDX)](../mdx/aggregate-mdx.md)   
 [Filter (MDX)](../mdx/filter-mdx.md)   
 [PrevMember (MDX)](../mdx/prevmember-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
