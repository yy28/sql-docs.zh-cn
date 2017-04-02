---
title: "EXISTING 关键字 (MDX) | Microsoft Docs"
ms.custom: ""
ms.date: "03/04/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "EXISTING"
helpviewer_keywords: 
  - "Existing 关键字"
ms.assetid: 651ee9ac-04ef-4316-87c9-a3df5ac27d22
caps.latest.revision: 38
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# EXISTING 关键字 (MDX)
  强制在当前上下文中计算所指定的集。  
  
## 语法  
  
```  
  
Existing Set_Expression  
```  
  
## 参数  
 *Set_Expression*  
 有效的多维表达式 (MDX) 集表达式。  
  
## 注释  
 默认情况下，在包含集成员的多维数据集的上下文中对集进行求值。 但 **Existing** 关键字强制在当前上下文中对指定的集进行求值。  
  
## 示例  
 下面的示例根据用 **Aggregate** 函数计算、用户选择的 State-Province 成员值，返回上一个时期销售额下滑的分销商的计数。 [Hierarchize (MDX)](../../../mdx/hierarchize-mdx.md) 和 [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md) 函数用于返回 Product 维度中产品类别的销售额下降值。 **Existing** 关键字强制在当前上下文中对 **Filter** 函数中的集求值，即对 State-Province 属性层次结构的 Washington 和 Oregon 成员求值。  
  
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
  
## 另请参阅  
 [Count（集）(MDX)](../../../mdx/count-set-mdx.md)   
 [AddCalculatedMembers (MDX)](../../../mdx/addcalculatedmembers-mdx.md)   
 [Aggregate (MDX)](../../../mdx/aggregate-mdx.md)   
 [Filter (MDX)](../../../mdx/filter-mdx.md)   
 [属性 (MDX)](../../../mdx/properties-mdx.md)   
 [DrilldownLevel (MDX)](../../../mdx/drilldownlevel-mdx.md)   
 [Hierarchize (MDX)](../../../mdx/hierarchize-mdx.md)   
 [MDX 函数引用 (MDX)](../../../mdx/mdx-function-reference-mdx.md)  
  
  