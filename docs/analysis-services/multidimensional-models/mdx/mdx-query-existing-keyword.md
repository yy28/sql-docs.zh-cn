---
title: "EXISTING 关键字 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords: EXISTING
helpviewer_keywords: Existing keyword
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: 5bc9a22779eba59b104b75587c8fb216218cdb10
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="mdx-query---existing-keyword"></a>MDX 查询-EXISTING 关键字
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]强制指定类型的值，设置要进行求值的当前上下文中。  
  
## <a name="syntax"></a>语法  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 有效的多维表达式 (MDX) 集表达式。  
  
## <a name="remarks"></a>注释  
 默认情况下，在包含集成员的多维数据集的上下文中对集进行求值。 但 **Existing** 关键字强制在当前上下文中对指定的集进行求值。  
  
## <a name="example"></a>示例  
 下面的示例根据用 **Aggregate** 函数计算、用户选择的 State-Province 成员值，返回上一个时期销售额下滑的分销商的计数。 但 [Hierarchize (MDX)](../../../mdx/hierarchize-mdx.md) 和 [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) 函数用于返回 Product 维度中产品类别的销售额下降值。 **Existing** 关键字强制在当前上下文中对 **Filter** 函数中的集求值，即对 State-Province 属性层次结构的 Washington 和 Oregon 成员求值。  
  
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
 [Count（集）(MDX)](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers &#40;MDX &#41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [聚合 &#40;MDX &#41;](../../../mdx/aggregate-mdx.md)   
 [筛选器 &#40;MDX &#41;](../../../mdx/filter-mdx.md)   
 [属性 &#40;MDX &#41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel &#40;MDX &#41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize &#40;MDX &#41;](../../../mdx/hierarchize-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
