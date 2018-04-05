---
title: LastPeriods (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- LASTPERIODS
dev_langs:
- kbMDX
helpviewer_keywords:
- LastPeriods function
ms.assetid: a15df7a1-b261-48ed-aacc-d2804db8dbf7
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: a3a9f0940796ecbc8138447fa8dd4ba59febbe96
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="lastperiods-mdx"></a>LastPeriods (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回指定成员之前（包含该成员）的成员集。  
  
## <a name="syntax"></a>语法  
  
```  
  
LastPeriods(Index [ ,Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Index*  
 指定期间数的有效数值表达式。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 如果指定的数量的段为正， **LastPeriods**函数将返回一组的成员以在成员开头*索引*-1 的指定的成员表达式，并以指定的成员结束。 成员函数返回的数目是否等于*索引*。  
  
 如果指定的数量的段为负， **LastPeriods**函数返回一组的成员、 指定的成员启动和结束的潜在顾客的成员 (-*索引*-1) 从指定的成员。 成员函数返回的数目是否等于绝对值的数值的*索引*。  
  
 如果指定的期间数为零， **LastPeriods**函数将返回空集。 这是与不同**延隔时间**函数，如果指定 0，则返回指定的成员。  
  
 如果未指定成员， **LastPeriods**函数使用**Time.CurrentMember**。 如果没有任何一个维度标记为 Time 维度，该函数将在不发生错误的情况下分析并执行，但将导致客户端应用程序出现单元错误。  
  
## <a name="examples"></a>示例  
 下面的示例返回 2002 会计年度第二、第三和第四会计季度的默认度量值。  
  
```  
SELECT LastPeriods(3,[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]) ON 0  
FROM [Adventure Works]  
```  
  
> [!NOTE]  
>  此示例还可以用 :（冒号）运算符编写：  
>   
>  `[Date].[Fiscal].[Fiscal Quarter].[Q4 FY 2002]: [Date].[Fiscal].[Fiscal Quarter].[Q2 FY 2002]`  
  
 下面的示例返回 2002 会计年度第一会计季度的默认度量值。 虽然指定的期间数为三个，但是只能返回一个，因为该会计年度中没有更早的期间。  
  
```  
SELECT LastPeriods  
   (3,[Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002]  
   ) ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
