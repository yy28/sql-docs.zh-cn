---
title: IIf （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 87b7b030776c1c18bb13307bf97db721fe472bd3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68105328"
---
# <a name="iif-mdx"></a>IIf (MDX)


  根据布尔条件为 true 还是 false，计算不同的分支表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>参数  
 IIf 函数使用三个参数： iif （\<condition>， \<then branch>， \<否则 branch>）。  
  
 *Logical_Expression*  
 计算结果为**true** （1）或**false** （0）的条件。 它必须是有效的多维表达式 (MDX) 逻辑表达式。  
  
 *表达式2提示 [渴望 |严格 |懒惰]]*  
 逻辑表达式计算结果为**true**时使用。 Expression1 必须是有效的多维表达式 (MDX) 表达式。  
  
 *表达式2提示 [渴望 |严格 |懒惰]]*  
 逻辑表达式的计算结果为**false**时使用。 Expression2 必须是有效的多维表达式 (MDX) 表达式。  
  
## <a name="remarks"></a>备注  
 如果此表达式的值为零，则逻辑表达式指定的条件的计算结果为**false** 。 任何其他值的计算结果为**true**。  
  
 当条件为**true**时， **IIf**函数返回第一个表达式。 否则，该函数返回第二个表达式。  
  
 指定的表达式可以返回值或 MDX 对象。 此外，指定表达式的类型无需匹配。  
  
 不建议使用**IIf**函数根据搜索条件创建一组成员。 请改用[筛选器](../mdx/filter-mdx.md)函数来针对逻辑表达式计算指定集中的每个成员，并返回成员的子集。  
  
> [!NOTE]  
>  如果任意一个表达式的计算结果为 NULL，则当满足该条件时，结果集为 NULL。  
  
 提示是一个可选修饰符，用于决定如何以及何时计算表达式。 它允许您通过指定计算表达式的方式来覆盖默认查询计划。  
  
-   EAGER 针对原始 IIF 子空间计算表达式。  
  
-   STRICT 仅在逻辑条件表达式创建的受限制子空间中计算表达式。  
  
-   LAZY 在逐个单元的模式下计算表达式。  
  
 EAGER 和 STRICT 仅应用于 IIF 的 then-else 分支，LAZY 则应用于所有 MDX 表达式。 任意 MDX 表达式可以后跟 HINT LAZY，后者在逐个单元的模式下计算该表达式。  
  
 在提示中，EAGER 和 STRICT 是互斥的；可以在不同表达式的相同 IIF(,,) 中使用它们。  
  
 有关详细信息，请参阅[IIF 函数查询提示](https://go.microsoft.com/fwlink/?LinkId=269540)，请参阅 SQL Server Analysis Services 2008 和[MDX IIF 函数和 CASE 语句的执行计划和计划提示](https://go.microsoft.com/fwlink/?LinkId=269565)。  
  
## <a name="examples"></a>示例  
 下面的查询显示在计算度量值中，在度量值 Internet 销售额大于或小于 $10000 时返回两个不同字符串值中的一个的**IIF**的简单用法：  
  
 `WITH MEMBER MEASURES.IIFDEMO AS`  
  
 `IIF([Measures].[Internet Sales Amount]>10000`  
  
 `, "Sales Are High", "Sales Are Low")`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.IIFDEMO} ON 0,`  
  
 `[Date].[Date].[Date].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
 IIF 的十分常见的用法是处理计算度量值内部的“被零除”错误，如以下示例所示：  
  
 `WITH`  
  
 `//Returns 1.#INF when the previous period contains no value`  
  
 `//but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth With Errors] AS`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `,FORMAT_STRING='PERCENT'`  
  
 `//Traps division by zero and returns null when the previous period contains`  
  
 `//no value but the current period does`  
  
 `MEMBER MEASURES.[Previous Period Growth] AS`  
  
 `IIF(([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)=0,`  
  
 `NULL,`  
  
 `([Measures].[Internet Sales Amount]-([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER))`  
  
 `/`  
  
 `([Measures].[Internet Sales Amount], [Date].[Date].CURRENTMEMBER.PREVMEMBER)`  
  
 `),FORMAT_STRING='PERCENT'`  
  
 `SELECT {[Measures].[Internet Sales Amount],MEASURES.[Previous Period Growth With Errors], MEASURES.[Previous Period Growth]} ON 0,`  
  
 `DESCENDANTS(`  
  
 `[Date].[Calendar].[Calendar Year].&[2004],`  
  
 `[Date].[Calendar].[Date])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 下面**的示例返回了**在生成函数内返回两个集合中的一个集合，以在行上创建一组复杂的元组：  
  
 `SELECT {[Measures].[Internet Sales Amount]} ON 0,`  
  
 `//If Internet Sales Amount is zero or null`  
  
 `//returns the current year and the All Customers member`  
  
 `//else returns the current year broken down by Country`  
  
 `GENERATE(`  
  
 `[Date].[Calendar Year].[Calendar Year].MEMBERS`  
  
 `, IIF([Measures].[Internet Sales Amount]=0,`  
  
 `{([Date].[Calendar Year].CURRENTMEMBER, [Customer].[Country].[All Customers])}`  
  
 `, {{[Date].[Calendar Year].CURRENTMEMBER} * [Customer].[Country].[Country].MEMBERS}`  
  
 `))`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 `WHERE([Product].[Product Categories].[Subcategory].&[26])`  
  
 最后，此示例显示如何使用计划提示：  
  
 `WITH MEMBER MEASURES.X AS`  
  
 `IIF(`  
  
 `[Measures].[Internet Sales Amount]=0`  
  
 `, NULL`  
  
 `, (1/[Measures].[Internet Sales Amount]) HINT EAGER)`  
  
 `SELECT {[Measures].x} ON 0,`  
  
 `[Customer].[Customer Geography].[Country].MEMBERS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
