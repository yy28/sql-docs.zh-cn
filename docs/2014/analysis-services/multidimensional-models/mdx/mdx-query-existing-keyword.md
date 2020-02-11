---
title: EXISTING 关键字（MDX） |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
f1_keywords:
- EXISTING
helpviewer_keywords:
- Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a6c5e8dbe3e1b1ad44286bcbb79132010cad618a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073969"
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
 默认情况下，在包含集成员的多维数据集的上下文中对集进行求值。 但 `Existing` 关键字强制在当前上下文中对指定的集进行求值。  
  
## <a name="example"></a>示例  
 下例将根据使用 `Aggregate` 函数求出并由用户选择的 State-Province 成员值，返回在上一时间段内销售额下降的分销商的计数。 但 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx) 和 [DrilldownLevel (MDX)](/sql/mdx/drilldownlevel-mdx) 函数用于返回 Product 维度中产品类别的销售额下降值。 `Existing`关键字强制在当前上下文中计算`Filter`函数集中的集，即州/省属性层次结构的华盛顿成员和俄勒冈成员。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [&#41; &#40;MDX&#41;&#40;集计数](/sql/mdx/count-set-mdx)   
 [AddCalculatedMembers &#40;MDX&#41;](/sql/mdx/addcalculatedmembers-mdx)   
 [聚合 &#40;MDX&#41;](/sql/mdx/aggregate-mdx)   
 [筛选 &#40;MDX&#41;](/sql/mdx/filter-mdx)   
 [MDX&#41;&#40;属性](/sql/mdx/properties-mdx)   
 [DrilldownLevel &#40;MDX&#41;](/sql/mdx/drilldownlevel-mdx)   
 [Hierarchize &#40;MDX&#41;](/sql/mdx/hierarchize-mdx)   
 [Mdx 函数引用 &#40;MDX&#41;](/sql/mdx/mdx-function-reference-mdx)  
  
  
