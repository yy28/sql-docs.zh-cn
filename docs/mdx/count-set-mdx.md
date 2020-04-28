---
title: Count （集）（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aac2f72cc8cd91e1964fd7734b858be8215cfdd8
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
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
 **计数（Set）** 函数包括或排除空单元，具体取决于所使用的语法。 如果使用标准语法，则可以分别使用**EXCLUDEEMPTY**或**INCLUDEEMPTY**标志排除或包含空单元。 如果使用备用语法，则函数始终包括空单元。  
  
 若要在集的计数中排除空单元，请使用标准语法和可选的**EXCLUDEEMPTY**标志。  
  
> [!NOTE]  
>  默认情况下， **Count （Set）** 函数对空单元进行计数。 相反，默认情况下，计算集数的 OLE DB 中的**Count**函数不包括空单元。  
  
## <a name="examples"></a>示例  
 下例统计成员集中单元的数目，该成员集由“产品”维度中“型号名称”属性层次结构的子级构成。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例通过将**DrilldownLevel**函数与**Count**函数结合使用来计算 Product 维度中的产品数。  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 下面的示例通过将**Count**函数与**Filter**函数以及其他许多函数结合使用，返回与前一个日历季度相比的销售额被下降的分销商。 此查询使用**聚合**函数来支持从客户端应用程序的下拉列表中选择多个地理成员（例如）。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [&#41; &#40;MDX&#41;&#40;维度计数](../mdx/count-dimension-mdx.md)   
 [&#41; &#40;MDX&#41;&#40;层次结构级别](../mdx/count-hierarchy-levels-mdx.md)   
 [&#41; &#40;MDX &#40;元组计数&#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40;MDX&#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40;MDX&#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize &#40;MDX&#41;](../mdx/hierarchize-mdx.md)   
 [MDX&#41;&#40;属性](../mdx/properties-mdx.md)   
 [聚合 &#40;MDX&#41;](../mdx/aggregate-mdx.md)   
 [筛选 &#40;MDX&#41;](../mdx/filter-mdx.md)   
 [PrevMember &#40;MDX&#41;](../mdx/prevmember-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
