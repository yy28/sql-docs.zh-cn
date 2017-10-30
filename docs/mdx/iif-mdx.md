---
title: "IIf (MDX) |Microsoft 文档"
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
- IIF
dev_langs:
- kbMDX
helpviewer_keywords:
- IIf function
ms.assetid: ec7b35e6-f4c5-40bf-93c8-b83c1cc26fe2
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 0b520aa3c3761c8dd8452b1732923b7415bcbca6
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="iif-mdx"></a>IIf (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  根据布尔条件为 true 还是 false，计算不同的分支表达式。  
  
## <a name="syntax"></a>语法  
  
```  
  
IIf(Logical_Expression, Expression1 [HINT <hints>], Expression2 [HINT <hints>])  
```  
  
## <a name="arguments"></a>参数  
 IIf 函数取三个参数： iif (\<条件 >，\<然后分支 >， \<else 分支 >)。  
  
 *Logical_Expression*  
 条件计算结果为**true** (1) 或**false** (0)。 它必须是有效的多维表达式 (MDX) 逻辑表达式。  
  
 *Expression1 提示 [Eager |严格 |延迟]]*  
 逻辑表达式计算结果为时使用**true**。 Expression1 必须是有效的多维表达式 (MDX) 表达式。  
  
 *Expression2 提示 [Eager |严格 |延迟]]*  
 逻辑表达式计算结果为时使用**false**。 Expression2 必须是有效的多维表达式 (MDX) 表达式。  
  
## <a name="remarks"></a>注释  
 逻辑表达式指定的条件的计算结果为**false**时此表达式的值为零。 任何其他值的计算结果为**true**。  
  
 满足条件时**true**、 **IIf**函数将返回第一个表达式。 否则，该函数返回第二个表达式。  
  
 指定的表达式可以返回值或 MDX 对象。 此外，指定表达式的类型无需匹配。  
  
 **IIf**函数不推荐使用来创建一组基于搜索条件的成员。 请改用[筛选器](../mdx/filter-mdx.md)函数来计算逻辑表达式针对一个指定集的每个成员并返回成员的子集。  
  
> [!NOTE]  
>  如果任意一个表达式的计算结果为 NULL，则当满足该条件时，结果集为 NULL。  
  
 提示是一个可选修饰符，用于决定如何以及何时计算表达式。 它允许您通过指定计算表达式的方式来覆盖默认查询计划。  
  
-   EAGER 针对原始 IIF 子空间计算表达式。  
  
-   STRICT 仅在逻辑条件表达式创建的受限制子空间中计算表达式。  
  
-   LAZY 在逐个单元的模式下计算表达式。  
  
 EAGER 和 STRICT 仅应用于 IIF 的 then-else 分支，LAZY 则应用于所有 MDX 表达式。 任意 MDX 表达式可以后跟 HINT LAZY，后者在逐个单元的模式下计算该表达式。  
  
 在提示中，EAGER 和 STRICT 是互斥的；可以在不同表达式的相同 IIF(,,) 中使用它们。  
  
 有关详细信息，请参阅[IIF 函数查询提示在 SQL Server Analysis Services 2008](http://go.microsoft.com/fwlink/?LinkId=269540)和[执行计划和计划提示 MDX IIF 函数以及 CASE 语句](http://go.microsoft.com/fwlink/?LinkId=269565)。  
  
## <a name="examples"></a>示例  
 以下查询显示了简单的用法**IIF**内计算度量值返回两个不同字符串值时度量值 Internet Sales Amount 大于或小于 $10000 之一：  
  
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
  
 以下是一种**IIF**返回要在行上创建一组复杂的元组的生成函数中的两个集之一：  
  
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
  
## <a name="see-also"></a>另請參閱  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  

