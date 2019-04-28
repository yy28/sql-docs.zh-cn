---
title: 计算上下文 |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 340d03ba8d0c5a66d89937627ab9389fc49abcae
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62807691"
---
# <a name="calculation-context"></a>计算上下文
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  计算上下文是多维数据集的已知子空间，在其中，将对表达式进行计算，并且所有坐标或者是显式已知的，或者可以从表达式派生。  
  
## <a name="determining-the-calculation-context"></a>确定计算上下文  
 每个集、成员、元组或数值函数均在整个 MDX 表达式或语句的上下文中执行。 当参数（例如元组）传递到函数时，仅显式提供多维数据集空间中的若干个坐标。 其他坐标根据当前计算上下文来获取。  
  
 按照以下顺序确定未指定的单元坐标和属性成员的计算上下文：  
  
1.  FROM 子句（如果适用）- 此子句可指定整个多维数据集，或以 SELECT 语句的形式指定子多维数据集。  
  
2.  WHERE 子句（如果适用）- 此子句也称为“切片器轴”，可在其上指定集、元组或成员以限制查询在列轴或行轴上返回成员。 从概念上来说，未在列轴或行轴上显式指定的每个属性层次结构的默认成员均是切片器轴的一部分。  
  
    > [!NOTE]  
    >  在切片器轴和其他轴上指定特定属性的单元坐标时，函数中指定的坐标可能优先确定轴上的集的成员。 [Filter (MDX)](../../../mdx/filter-mdx.md) 和 [Order (MDX)](../../../mdx/order-mdx.md) 函数是这类函数的示例 - 你可以按属性成员（通过 WHERE 子句或 FROM 子句中的 SELECT 语句排除在计算上下文之外）对结果进行筛选或排序。  
  
3.  在查询或表达式中定义的命名集和计算成员。  
  
4.  在行轴和列轴上指定的元组和集，对没有显示在行轴、列轴或切片器轴上的属性使用默认成员。  
  
5.  每个轴上的多维数据集或子多维数据集，消除了轴上的空元组并应用 HAVING 子句。  
  
6.  有关详细信息，请参阅 [在查询中建立多维数据集上下文 (MDX)](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)。  
  
 在以下查询中，由 WHERE 子句中指定的 Country 属性成员和 Calendar Year 属性成员限制行轴的计算上下文。  
  
```  
SELECT Customer.City.City.Members ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France, [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 如果通过在行轴上指定 **FILTER** 函数修改此查询，并在 **FILTER** 函数中使用 Calendar Year 属性层次结构成员，则可以修改 Calendar Year 属性层次结构中的属性成员（用于为列轴上的集的成员提供计算上下文）。  
  
```  
SELECT FILTER  
   (  
      Customer.City.City.Members,   
         ([Date].[Calendar].[Calendar Year].[CY 2003],  
            Measures.[Internet Order Quantity]) > 75   
   ) ON 0  
FROM [Adventure Works]  
WHERE (Customer.Country.France,  
   [Date].[Calendar].[Calendar Year].[CY 2004],  
   Measures.[Internet Sales Amount])  
```  
  
 在前面的查询中，由 Calendar Year 属性层次结构的 CY 2003 成员筛选列轴上所显示元组的单元的计算上下文，即便 Calendar Year 属性层次结构名义上的计算上下文为 CY 2004 也是如此。 另外，它由 Internet Order Quantity 度量值筛选。 不过，只要设置了列轴上的集成员，就将再次由 WHERE 子句确定显示在该轴上的成员值的计算上下文。  
  
> [!IMPORTANT]  
>  若要提高查询性能，应在解析过程中尽早地消除成员和元组。 通过这种方式，针对最终成员集的复杂查询时间计算涉及的单元最少。  
  
## <a name="see-also"></a>请参阅  
 [在查询中建立多维数据集上下文 (MDX)](../../../analysis-services/multidimensional-models/mdx/establishing-cube-context-in-a-query-mdx.md)   
 [MDX 查询基础知识 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/mdx-query-fundamentals-analysis-services.md)   
 [MDX 中的重要概念 (Analysis Services)](../../../analysis-services/multidimensional-models/mdx/key-concepts-in-mdx-analysis-services.md)  
  
  
