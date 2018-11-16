---
title: IIf (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0b05929d24533e0bdcdbcac59820307a373428ff
ms.sourcegitcommit: 50b60ea99551b688caf0aa2d897029b95e5c01f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51700775"
---
# <a name="iif-mdx"></a>IIf (MDX)


  根据布尔条件为 true 还是 false，计算不同的分支表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>参数  
 IIf 函数有三个参数： iif (\<条件 >，\<分支 >， \<else 分支 >)。  
  
 *Logical_Expression*  
 条件的计算结果为 **，则返回 true** (1) 或**false** (0)。 它必须是有效的多维表达式 (MDX) 逻辑表达式。  
  
 *Expression1 提示 [预先 |严格 |延迟]]*  
 逻辑表达式的计算结果时使用 **，则返回 true**。 Expression1 必须是有效的多维表达式 (MDX) 表达式。  
  
 *Expression2 提示 [预先 |严格 |延迟]]*  
 逻辑表达式的计算结果时使用**false**。 Expression2 必须是有效的多维表达式 (MDX) 表达式。  
  
## <a name="remarks"></a>备注  
 逻辑表达式指定的条件计算结果为**false**时此表达式的值为零。 任何其他值的计算结果为 **，则返回 true**。  
  
 条件何时 **，则返回 true**，则**IIf**函数将返回第一个表达式。 否则，该函数返回第二个表达式。  
  
 指定的表达式可以返回值或 MDX 对象。 此外，指定表达式的类型无需匹配。  
  
 **IIf**函数不建议用于创建基于搜索条件的成员集。 请改用[筛选器](../mdx/filter-mdx.md)函数来计算逻辑表达式对指定集中每个成员并返回成员的子集。  
  
> [!NOTE]  
>  如果任意一个表达式的计算结果为 NULL，则当满足该条件时，结果集为 NULL。  
  
 提示是一个可选修饰符，用于决定如何以及何时计算表达式。 它允许您通过指定计算表达式的方式来覆盖默认查询计划。  
  
-   EAGER 针对原始 IIF 子空间计算表达式。  
  
-   STRICT 仅在逻辑条件表达式创建的受限制子空间中计算表达式。  
  
-   LAZY 在逐个单元的模式下计算表达式。  
  
 EAGER 和 STRICT 仅应用于 IIF 的 then-else 分支，LAZY 则应用于所有 MDX 表达式。 任意 MDX 表达式可以后跟 HINT LAZY，后者在逐个单元的模式下计算该表达式。  
  
 在提示中，EAGER 和 STRICT 是互斥的；可以在不同表达式的相同 IIF(,,) 中使用它们。  
  
 有关详细信息，请参阅[SQL Server Analysis Services 2008 中的 IIF 函数查询提示](https://go.microsoft.com/fwlink/?LinkId=269540)并[执行计划和计划提示 MDX IIF 函数和 CASE 语句](https://go.microsoft.com/fwlink/?LinkId=269565)。  
  
## <a name="examples"></a>示例  
 以下查询说明的简单用法**IIF**内计算度量值返回两个不同的字符串值时度量值 Internet Sales Amount 大于或小于 $10000 之一：  
  
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
  
 以下是一种**IIF**返回的行上创建一组复杂的元组在 Generate 函数内部的两个集之一：  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
