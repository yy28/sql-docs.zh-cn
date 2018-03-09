---
title: "非空 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: NonEmpty function
ms.assetid: dfbfa747-3175-405c-aa5b-15c187b06338
caps.latest.revision: "17"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: a17e8cf51ac2c2a8bac98315b85f53421d7c3c4b
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="nonempty-mdx"></a>NonEmpty (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  根据第一个指定集与第二个集的叉积，返回指定集中的非空元组集。  
  
## <a name="syntax"></a>语法  
  
```  
  
NONEMPTY(set_expression1 [,set_expression2])  
```  
  
## <a name="arguments"></a>参数  
 *set_expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *set_expression2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 此函数返回位于第一个指定集中并且在对第二个集中的元组求值时不为空的元组。 **NonEmpty**函数将考虑帐户计算和保留了重复元组。 如果未提供第二个集，将在多维数据集中属性层次结构和度量值的成员的当前坐标上下文中对表达式求值。  
  
> [!NOTE]  
>  使用此函数而不是不推荐使用[NonEmptyCrossjoin &#40;MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)函数。  
  
> [!IMPORTANT]  
>  非空是元组所引用的单元的特征，而不是元组本身的特征。  
  
## <a name="examples"></a>示例  
 以下查询显示的一个简单示例**NonEmpty**，返回具有用于 Internet Sales Amount 的非 null 值，2001 年 7 月 1 日的所有客户：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `NONEMPTY(`  
  
 `[Customer].[Customer].[Customer].MEMBERS`  
  
 `, {([Date].[Calendar].[Date].&[20010701], [Measures].[Internet Sales Amount])}`  
  
 `)`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 下面的示例返回包含客户和购买日期，使用元组的一套**筛选器**函数和**NonEmpty**函数来查找每个客户购买过的最后日期：  
  
 `WITH SET MYROWS AS FILTER`  
  
 `(NONEMPTY`  
  
 `([Customer].[Customer Geography].[Customer].MEMBERS`  
  
 `* [Date].[Date].[Date].MEMBERS`  
  
 `, [Measures].[Internet Sales Amount]`  
  
 `) AS MYSET`  
  
 `, NOT(MYSET.CURRENT.ITEM(0)`  
  
 `IS MYSET.ITEM(RANK(MYSET.CURRENT, MYSET)).ITEM(0))`  
  
 `)`  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `MYROWS ON 1`  
  
 `FROM [Adventure Works]`  
  
## <a name="see-also"></a>另请参阅  
 [DefaultMember &#40;MDX &#41;](../mdx/defaultmember-mdx.md)   
 [筛选器 &#40;MDX &#41;](../mdx/filter-mdx.md)   
 [IsEmpty &#40;MDX &#41;](../mdx/isempty-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [NonEmptyCrossjoin &#40;MDX &#41;](../mdx/nonemptycrossjoin-mdx.md)  
  
  
