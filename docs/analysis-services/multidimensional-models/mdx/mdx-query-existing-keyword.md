---
title: EXISTING 关键字 (MDX) |Microsoft 文档
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 65d9bfc708c79e1979f0fd423bc99dfafa37def0
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="mdx-query---existing-keyword"></a>MDX 查询-EXISTING 关键字
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  强制在当前上下文中计算所指定的集。  
  
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
 [计数 & #40;集 & #41;& #40;MDX & #41;](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers & #40;MDX & #41;](../../../mdx/addcalculatedmembers-mdx.md)   
 [聚合 & #40;MDX & #41;](../../../mdx/aggregate-mdx.md)   
 [筛选器 & #40;MDX & #41;](../../../mdx/filter-mdx.md)   
 [属性 & #40;MDX & #41;](../../../mdx/properties-mdx.md)   
 [DrilldownLevel & #40;MDX & #41;](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize & #40;MDX & #41;](../../../mdx/hierarchize-mdx.md)   
 [MDX 函数引用 & #40;MDX & #41;](../../../mdx/mdx-function-reference-mdx.md)  
  
  
