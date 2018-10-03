---
title: EXISTING 关键字 (MDX) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 8431c4b29f20b3c87e3b944736612d009426900a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106547"
---
# <a name="existing-keyword-mdx"></a>EXISTING 关键字 (MDX)
  强制在当前上下文中计算所指定的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 有效的多维表达式 (MDX) 集表达式。  
  
## <a name="remarks"></a>备注  
 默认情况下，在包含集成员的多维数据集的上下文中对集进行求值。 `Existing`关键字强制指定的集计算当前上下文中。  
  
## <a name="example"></a>示例  
 下例将根据使用 `Aggregate` 函数求出并由用户选择的 State-Province 成员值，返回在上一时间段内销售额下降的分销商的计数。 但 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) 和 [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) 函数用于返回 Product 维度中产品类别的销售额下降值。 `Existing`关键字强制在集`Filter`函数将计算当前上下文-也就是说，在针对 State-province 属性层次结构的 Washington 和 Oregon 成员。  
  
```  
WITH MEMBER Measures.[Declining Reseller Sales] AS  
   Count  
      (Filter  
         (Existing  
            (Reseller.Reseller.Reseller)  
         , [Measures].[Reseller Sales Amount] <   
            ([Measures].[Reseller Sales Amount]  
               ,[Date].Calendar.PrevMember  
            )  
        )  
      )  
MEMBER [Geography].[State-Province].x AS   
   Aggregate   
      ( {[Geography].[State-Province].&[WA]&[US]  
         , [Geography].[State-Province].&[OR]&[US] }   
      )  
SELECT NON EMPTY HIERARCHIZE   
      (AddCalculatedMembers   
         (   
            {DrillDownLevel  
               ({[Product].[All Products]}  
               )  
            }   
         )   
      ) DIMENSION PROPERTIES PARENT_UNIQUE_NAME ON COLUMNS   
FROM [Adventure Works]  
WHERE   
      ( [Geography].[State-Province].x  
        , [Date].[Calendar].[Calendar Quarter].&[2003]&[4]  
        ,[Measures].[Declining Reseller Sales]  
      )  
  
```  
  
## <a name="see-also"></a>请参阅  
 [计数&#40;设置&#41; &#40;MDX&#41;](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers &#40;MDX&#41;](/sql/mdx/addcalculatedmembers-mdx)   
 [聚合&#40;MDX&#41;](/sql/mdx/aggregate-mdx)   
 [筛选器&#40;MDX&#41;](/sql/mdx/filter-mdx)   
 [属性&#40;MDX&#41;](/sql/mdx/properties-mdx)   
 [DrilldownLevel &#40;MDX&#41;](/sql/mdx/drilldownlevel-mdx)   
 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx)   
 [MDX 函数引用&#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
