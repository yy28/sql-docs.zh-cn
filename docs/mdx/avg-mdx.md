---
title: Avg （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: aa8817e35a589def4631bd455637d05fc62d3a0f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68017011"
---
# <a name="avg-mdx"></a>Avg (MDX)


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
  
## <a name="remarks"></a>备注  
 如果指定了一组空元组或空集，则**Avg**函数将返回空值。  
  
 **Avg**函数通过首先计算指定集中单元的值之和来计算指定集中单元的非空值的平均值，然后将计算所得的和除以指定集内的非空单元计数。  
  
> [!NOTE]  
>  计算一组数值的平均值时，[!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] 将忽略 Null 值。  
  
 如果未指定特定的数值表达式（通常为度量值），则**Avg**函数将计算当前查询上下文中每个度量值的平均值。 如果提供了特定的度量值，则**Avg**函数首先计算该集的度量值，然后该函数基于指定的度量值计算平均值。  
  
> [!NOTE]  
>  在计算成员语句中使用**CurrentMember**函数时，必须指定数值表达式，因为在此类查询上下文中不存在当前坐标的默认度量值。  
  
 若要强制包含空单元格，应用程序必须使用[CoalesceEmpty](../mdx/coalesceempty-mdx.md)函数，或指定有效的*Numeric_Expression* ，为空值提供值零（0）。 有关空单元的详细信息，请参阅 OLE DB 文档。  
  
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
  
 下面的示例返回`Measures.[Gross Profit Margin]`度量值的每日平均值，该度量值是通过来自**艾德公司**的2003会计年度中每个月的几天计算得出的。 **Avg**函数计算`[Ship Date].[Fiscal Time]`层次结构每个月中包含的一组天数中的平均值。 第一种形式的计算演示 Avg 将未记录任何销售额的天数从平均值计算中排除的默认行为，第二种形式的计算演示如何将没有销售额的天数包含在平均值计算中。  
  
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
  
 下面的示例返回`Measures.[Gross Profit Margin]`度量值的日平均值，该度量值是通过来自**艾德公司**的每个学期的每个半2003期计算得出的。  
  
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
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
