---
title: EXISTING 关键字 (MDX) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d41b49e4585d2a256250a009b09ffa9ed94ea925
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68208734"
---
# <a name="mdx-query---existing-keyword"></a>MDX 查询 - EXISTING 关键字
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  强制在当前上下文中计算所指定的集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Existing Set_Expression  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 有效的多维表达式 (MDX) 集表达式。  
  
## <a name="remarks"></a>备注  
 默认情况下，在包含集成员的多维数据集的上下文中对集进行求值。 但 **Existing** 关键字强制在当前上下文中对指定的集进行求值。  
  
## <a name="example"></a>示例  
 下面的示例根据用 **Aggregate** 函数计算、用户选择的 State-Province 成员值，返回上一个时期销售额下滑的分销商的计数。 但 [Hierarchize (MDX)](../../../mdx/hierarchize-mdx.md) 和 [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) 函数用于返回 Product 维度中产品类别的销售额下降值。 **Existing**关键字强制在集**筛选器**函数将计算当前上下文-也就是说，在针对 State-province 属性层次结构的 Washington 和 Oregon 成员。  
  
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
 [Count（集）(MDX)](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers (MDX)](../../../mdx/addcalculatedmembers-mdx.md)   
 [Aggregate (MDX)](../../../mdx/aggregate-mdx.md)   
 [Filter (MDX)](../../../mdx/filter-mdx.md)   
 [属性 (MDX)](../../../mdx/properties-mdx.md)   
 [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize (MDX)](../../../mdx/hierarchize-mdx.md)   
 [MDX 函数引用 (MDX)](../../../mdx/mdx-function-reference-mdx.md)  
  
  
