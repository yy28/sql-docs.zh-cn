---
title: "Avg (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AVG
dev_langs:
- kbMDX
helpviewer_keywords:
- Avg function [MDX]
ms.assetid: efe61272-c3eb-4a33-b231-e00c30be16aa
caps.latest.revision: 42
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: a0393bc578fd7c4f5b470ced1bb682755483f448
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="avg-mdx"></a>Avg (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  对集求值，并返回该集中的单元的非空值的平均值，此平均值是对该集中的度量值或指定度量值求得的平均值。  
  
## <a name="syntax"></a>语法  
  
```  
  
Avg( Set_Expression [ , Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 如果指定一组空元组或一个空集，则**Avg**函数将返回空值。  
  
 **Avg**函数将首先计算跨交集中的单元格的值的总和，然后将计算的总和除以交集中的非空单元格的计数来计算指定集的单元格的非空值的平均值。  
  
> [!NOTE]  
>  计算一组数值的平均值时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将忽略 Null 值。  
  
 如果未指定特定的数值表达式 （通常为量值）， **Avg**函数计算当前的查询上下文中每个度量值的平均值。 如果提供的特定度量值，则**Avg**函数在集合中，将首先计算度量值，然后该函数计算基于指定的度量值的平均值。  
  
> [!NOTE]  
>  使用时**CurrentMember**函数在计算的成员语句中，您必须指定数值表达式，因为没有默认度量值存在此类查询上下文中的当前坐标。  
  
 若要强制包含空单元格，应用程序必须使用[CoalesceEmpty](../mdx/coalesceempty-mdx.md)函数，或指定有效的*Numeric_Expression* ，它提供一个值为零 (0)，空值。 有关空单元的详细信息，请参阅 OLE DB 文档。  
  
## <a name="examples"></a>示例  
 下面的示例对指定集返回度量值的平均值。 请注意，指定度量值可以是指定集的成员的默认度量值，也可以是指定的度量值。  
  
 `WITH SET [NW Region] AS`  
  
 `{[Geography].[State-Province].[Washington]`  
  
 `, [Geography].[State-Province].[Oregon]`  
  
 `, [Geography].[State-Province].[Idaho]}`  
  
 `MEMBER [Geography].[Geography].[NW Region Avg] AS`  
  
 `AVG ([NW Region]`  
  
 `--Uncomment the line below to get an average by Reseller Gross Profit Margin`  
  
 `--otherwise the average will be by whatever the default measure is in the cube,`  
  
 `--or whatever measure is specified in the query`  
  
 `--, [Measures].[Reseller Gross Profit Margin]`  
  
 `)`  
  
 `SELECT [Date].[Calendar Year].[Calendar Year].Members ON 0`  
  
 `FROM [Adventure Works]`  
  
 `WHERE ([Geography].[Geography].[NW Region Avg])`  
  
 下面的示例返回的每日平均值`Measures.[Gross Profit Margin]`度量值，从计算在 2003年会计年度中，在每月的天数**Adventure Works**多维数据集。 **Avg**函数计算的每个月内包含的天的集的平均值`[Ship Date].[Fiscal Time]`层次结构。 第一种形式的计算演示 Avg 将未记录任何销售额的天数从平均值计算中排除的默认行为，第二种形式的计算演示如何将没有销售额的天数包含在平均值计算中。  
  
 `WITH MEMBER Measures.[Avg Gross Profit Margin] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `Measures.[Gross Profit Margin]`  
  
 `), format_String='percent'`  
  
 `MEMBER Measures.[Avg Gross Profit Margin Including Empty Days] AS`  
  
 `Avg(`  
  
 `Descendants(`  
  
 `[Ship Date].[Fiscal].CurrentMember,`  
  
 `[Ship Date].[Fiscal].[Date]`  
  
 `),`  
  
 `CoalesceEmpty(Measures.[Gross Profit Margin],0)`  
  
 `), Format_String='percent'`  
  
 `SELECT`  
  
 `{Measures.[Avg Gross Profit Margin],Measures.[Avg Gross Profit Margin Including Empty Days]} ON COLUMNS,`  
  
 `[Ship Date].[Fiscal].[Fiscal Year].Members ON ROWS`  
  
 `FROM`  
  
 `[Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Product].&[344])`  
  
 下面的示例返回的每日平均值`Measures.[Gross Profit Margin]`度量值，从贯穿 2003年会计年度中，在每个半期天数中计算出**Adventure Works**多维数据集。  
  
```  
WITH MEMBER Measures.[Avg Gross Profit Margin] AS  
   Avg(  
      Descendants(  
         [Ship Date].[Fiscal].CurrentMember,   
            [Ship Date].[Fiscal].[Date]  
      ),   
      Measures.[Gross Profit Margin]  
   )  
SELECT  
   Measures.[Avg Gross Profit Margin] ON COLUMNS,  
      [Ship Date].[Fiscal].[Fiscal Year].[FY 2003].Children ON ROWS  
FROM  
   [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

