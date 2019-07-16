---
title: 理解传递次序和求解次序 (MDX) |Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6a578537f5221fef314a4a732f00f99d82311bbe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "68176573"
---
# <a name="mdx-data-manipulation---understanding-pass-order-and-solve-order"></a>MDX 数据操作-了解传递顺序和求解次序
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  当某个多维数据集是 MDX 脚本的计算结果时，该多维数据集可能会经历许多计算阶段，具体取决于与计算有关的各种功能的使用情况。 每个阶段称为一个计算传递。  
  
 计算传递可以按序号位置（称为“计算传递号”）进行引用。 完全计算一个多维数据集中的所有单元所需的计算传递数称为多维数据集的计算传递深度。  
  
 事实数据表和写回数据仅影响传递 0。 脚本将在传递 0 后填充数据，脚本中的每一个赋值和计算语句都将创建一个新的传递。 在 MDX 脚本外，对绝对传递 0 的引用将引用脚本为多维数据集创建的最后一个传递。  
  
 在所有传递中都会创建计算成员，但表达式只应用于当前传递。 之前的传递包含计算度量值，但是值为空。  
  
## <a name="solve-order"></a>求解次序  
 求解次序决定了出现相互竞争的表达式时的计算优先级。 在一个传递中，求解次序决定了两点：  
  
-   [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 计算维度、成员、计算成员、自定义汇总和计算单元的次序。  
  
-   [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 计算自定义成员、计算成员、自定义汇总和计算单元的次序。  
  
 具有最高求解次序的成员优先。  
  
> [!NOTE]  
>  此优先级的例外情况是聚合函数。 与聚合函数一起使用的计算成员的求解次序比任何相交的计算度量值都低。  
  
## <a name="solve-order-values-and-precedence"></a>求解次序值和优先级  
 求解次序值的范围为 -8181 到 65535。 在此范围内，有些求解次序值对应于特定类型的计算，如下表所示。  
  
|计算|求解次序|  
|-----------------|-----------------|  
|自定义成员公式|-5119|  
|一元运算符|-5119|  
|直观合计计算|-4096|  
|所有其他计算（如果没有另行指定）|0|  
  
 强烈建议设置求解次序值时仅使用正整数。 如果赋值小于上表中所示的求解次序值，计算传递可能会变得不可预知。 例如，计算成员的计算接收的求解次序值小于默认自定义汇总公式值 -5119。 这样一个低的求解次序值会导致计算成员在自定义汇总公式之前计算，并产生错误的结果。  
  
### <a name="creating-and-changing-solve-order"></a>创建和更改求解次序  
 在多维数据集设计器的 **“计算”** 窗格上，可以通过更改计算顺序来更改计算成员和计算单元的求解次序。  
  
 在 MDX 中，可以使用 **SOLVE_ORDER** 关键字来创建或更改计算成员和计算单元。  
  
## <a name="solve-order-examples"></a>求解次序示例  
 为了说明求解次序可能具有的复杂性，下面的系列 MDX 查询将以两个本身没有求解次序问题的查询开始， 然后将这两个查询合并成一个需要求解次序的查询。  
  
> [!NOTE]  
>  您可以针对 Adventure Works 示例多维数据库运行这些 MDX 查询。 可以从 codeplex 站点下载 [AdventureWorks 多维模型 SQL Server 2012](http://msftdbprodsamples.codeplex.com/releases/view/55330) 示例。  
  
### <a name="query-1-differences-in-income-and-expenses"></a>查询 1-收入与支出的差异  
 对于第一个 MDX 查询，通过构造一个与以下示例类似的简单 MDX 查询，计算每年的销售与成本之间的差额：  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] )  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 在此查询中，只有一个计算成员 `Year Difference`。 因为只有一个计算成员，所以只要多维数据集不使用任何计算成员，求解次序就不是问题。  
  
 此 MDX 查询将生成一个类似于下表的结果集。  
  
||Internet Sales Amount|Internet Total Product Cost|  
|-|---------------------------|---------------------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|  
|**Year Difference**|($20,160.56)|$2,878.06|  
  
### <a name="query-2-percentage-of-income-after-expenses"></a>查询 2-支出后的收益百分比  
 对于第二个查询，通过使用下面的 MDX 查询，计算每年扣除支出后的收益百分比：  
  
```  
WITH   
MEMBER  
[Measures].[Profit Margin] AS   
([Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent"  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 与上一个查询类似，此 MDX 查询只有一个计算成员 `Profit Margin`，因此也不会有任何求解次序问题。  
  
 此 MDX 查询将生成一个类似于下表的略有不同的结果集。  
  
||Internet Sales Amount|Internet Total Product Cost|Profit Margin|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
  
 第一个查询与第二个查询在结果集方面的差异来自计算成员位置的不同。 在第一个查询中，计算成员是 ROWS 轴的一部分，而在第二个查询中，计算成员是 COLUMNS 轴的一部分。 下一个查询将两个计算成员合并到一个 MDX 查询中，这种位置上的不同在这个查询中就会变得非常重要。  
  
### <a name="query-3-combined-year-difference-and-net-income-calculations"></a>查询 3 组合年差额和净收益计算  
 在最后这个查询中，将上面两个示例合并成一个 MDX 查询，此时由于要同时对列和行进行计算，因此求解次序变得重要起来。 为了确保按正确的顺序进行计算，请使用 **SOLVE_ORDER** 关键字定义计算顺序。  
  
 **SOLVE_ORDER** 关键字指定 MDX 查询或 **CREATE MEMBER** 命令中计算成员的求解次序。 **SOLVE_ORDER** 关键字使用的整数值是相对的，不要求从零开始，也不要求是连续的。 该值只是告诉 MDX 基于通过计算具有较大求解次序值的成员得出的值来计算成员。 如果不使用 **SOLVE_ORDER** 关键字定义计算成员，计算成员的默认值将为零。  
  
 例如，如果合并前面两个查询示例中使用的计算，则两个计算成员 `Year Difference` 和 `Profit Margin`将相交于 MDX 查询示例的结果数据集中的一个单元中。 确定 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 如何计算此单元的唯一方式是通过求解次序。 根据两个计算成员的求解次序，用于构造此单元的公式将生成不同的结果。  
  
 首先，尝试将前面两个查询中使用的计算合并到下面的 MDX 查询中：  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 1  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 2  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 在这个合并的 MDX 查询示例中， `Profit Margin` 具有最高的求解次序，因此当两个表达式会相互影响时，它具有优先权。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用 `Profit Margin` 公式计算相关的单元。 此嵌套计算的结果如下表所示。  
  
||Internet Sales Amount|Internet Total Product Cost|Profit Margin|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Year Difference**|($20,160.56)|$2,878.06|114.28%|  
  
 共享单元中的结果基于 `Profit Margin`所用的公式。 也就是说， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 使用 `Year Difference` 数据计算共享单元中的结果，这样就会得到以下公式（为清楚起见，对结果进行了舍入）：  
  
```  
((9,770,899.74 - 9,791,060.30) - (5,721,205.24 - 5,718,327.17)) / (9,770,899.74 - 9,791,060.30) = 1.14275744   
```  
  
 或  
  
```  
(23,038.63) / (20,160.56) = 114.28%  
```  
  
 这明显是错误的。 但是，如果您切换了 MDX 查询中计算成员的求解次序， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将以不同的方式计算共享单元中的结果。 下面合并的 MDX 查询反转了计算成员的求解次序：  
  
```  
WITH   
MEMBER  
[Date].[Calendar].[Year Difference] AS ([Date].[Calendar].[Calendar Year].&[2008] - [Date].[Calendar].[Calendar Year].&[2007] ) ,  
SOLVE_ORDER = 2  
MEMBER  
[Measures].[Profit Margin] AS   
( [Measures].[Internet Sales Amount] - [Measures].[Internet Total Product Cost] ) / [Measures].[Internet Sales Amount] ,  
FORMAT_STRING="Percent" ,  
SOLVE_ORDER = 1  
SELECT   
{[Measures].[Internet Sales Amount], [Measures].[Internet Total Product Cost], [Measures].[Profit Margin] }  
ON COLUMNS ,  
{ [Date].[Calendar].[Calendar Year].&[2007], [Date].[Calendar].[Calendar Year].&[2008], [Date].[Year Difference] }  
ON ROWS  
FROM [Adventure Works]  
```  
  
 由于已经切换了计算成员的求解次序，因此 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将使用 `Year Difference` 公式来计算此单元，如下表所示。  
  
||Internet Sales Amount|Internet Total Product Cost|Profit Margin|  
|-|---------------------------|---------------------------------|-------------------|  
|**CY 2007**|$9,791,060.30|$5,718,327.17|41.60%|  
|**CY 2008**|$9,770,899.74|$5,721,205.24|41.45%|  
|**Year Difference**|($20,160.56)|$2,878.06|(0.15%)|  
  
 因为此查询对 `Year Difference` 数据使用 `Profit Margin` 公式，所以共享单元的公式与以下计算类似：  
  
```  
(($9,770,899.74 - 5,721,205.24) / $9,770,899.74) - ((9,791,060.30 - 5,718,327.17) / 9,791,060.30) = -0.15   
```  
  
 或  
  
```  
0.4145 - 0.4160= -0.15  
```  
  
## <a name="additional-considerations"></a>其他注意事项  
 求解次序可能会成为需要处理的非常复杂的问题，尤其是在具有很多维度而维度涉及计算成员、自定义汇总公式或计算单元的多维数据集中，更是如此。 当 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 计算 MDX 查询时， [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将考虑给定传递中涉及的所有内容的求解次序值，包括 MDX 查询中指定的多维数据集的维度。  
  
## <a name="see-also"></a>请参阅  
 [CalculationCurrentPass (MDX)](../../../mdx/calculationcurrentpass-mdx.md)   
 [CalculationPassValue (MDX)](../../../mdx/calculationpassvalue-mdx.md)   
 [CREATE MEMBER 语句 (MDX)](../../../mdx/mdx-data-definition-create-member.md)   
 [操作数据 (MDX)](../../../analysis-services/multidimensional-models/mdx/mdx-data-manipulation-manipulating-data.md)  
  
  
