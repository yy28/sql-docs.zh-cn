---
title: "计数 (Set) (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: 22f530e9-f8e1-4608-affa-9a2bc0821591
caps.latest.revision: "39"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 41d5ff72346e95985b19812f194d266e8d5db165
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="count-set-mdx"></a>Count（集）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
## <a name="remarks"></a>Remarks  
 **计数 (Set)**函数包括或排除空单元格，具体取决于所使用的语法。 如果使用标准的语法，则可排除或通过使用包含空单元格**EXCLUDEEMPTY**或**INCLUDEEMPTY**标记，分别。 如果使用备用语法，则函数始终包括空单元。  
  
 若要排除的一组数中的空单元格，请使用标准的语法和可选**EXCLUDEEMPTY**标志。  
  
> [!NOTE]  
>  **计数 (Set)**函数对空单元格默认情况下进行计数。 与此相反，**计数**函数在 OLE DB 用于计算一组默认情况下不包括空单元格。  
  
## <a name="examples"></a>示例  
 下例统计成员集中单元的数目，该成员集由“产品”维度中“型号名称”属性层次结构的子级构成。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Model Name].children.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
 下面的示例通过使用计算产品维度中的产品数**DrilldownLevel**函数结合**计数**函数。  
  
```  
Count(DrilldownLevel (   
   [Product].[Product].[Product]))  
```  
  
 下面的示例返回与拒绝销售到以前的日历季度，通过使用比较这些经销商**计数**函数结合**筛选器**函数和许多其他功能。 此查询使用**聚合**功能，以支持所选内容的多个地理位置成员，如从客户端应用程序中的下拉列表内的选择。  
  
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
 [计数 &#40; 维度 &#41;&#40;MDX &#41;](../mdx/count-dimension-mdx.md)   
 [计数 &#40;层次结构级别 &#41;&#40;MDX &#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [计数 &#40;元组 &#41;&#40;MDX &#41;](../mdx/count-tuple-mdx.md)   
 [DrilldownLevel &#40;MDX &#41;](../mdx/drilldownlevel-mdx.md)   
 [AddCalculatedMembers &#40;MDX &#41;](../mdx/addcalculatedmembers-mdx.md)   
 [Hierarchize &#40;MDX &#41;](../mdx/hierarchize-mdx.md)   
 [属性 &#40;MDX &#41;](../mdx/properties-mdx.md)   
 [聚合 &#40;MDX &#41;](../mdx/aggregate-mdx.md)   
 [筛选器 &#40;MDX &#41;](../mdx/filter-mdx.md)   
 [PrevMember &#40;MDX &#41;](../mdx/prevmember-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
