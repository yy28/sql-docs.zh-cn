---
title: "TopCount (MDX) |Microsoft 文档"
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
f1_keywords: TOPCOUNT
dev_langs: kbMDX
helpviewer_keywords: TopCount function
ms.assetid: 15026a8f-35c5-4307-8856-348f5c44bfd5
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: e68a27c85dde732a54b87e914b643565d8549933
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="topcount-mdx"></a>TopCount (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  按降序对集进行排序，并返回指定数目的最大值元素。  
  
## <a name="syntax"></a>语法  
  
```  
  
TopCount(Set_Expression,Count [ ,Numeric_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
 *计数*  
 指定要返回的元组数的有效数值表达式。  
  
 *Numeric_Expression*  
 返回数字的有效数值表达式，通常为单元坐标的多维表达式 (MDX)。  
  
## <a name="remarks"></a>Remarks  
 如果指定数值表达式，则**TopCount**函数以降序顺序，指定通过根据指定的数值表达式的值指定一组为指定集求得集中的元组排序。 对集进行排序之后**TopCount**函数然后返回指定的数目的具有最高值的元组。  
  
> [!IMPORTANT]  
>  如[BottomCount](../mdx/bottomcount-mdx.md)函数， **TopCount**函数始终中断层次结构。  
  
 如果未指定数值表达式，函数将返回成员组成的集在自然顺序排序，不进行任何排序，如行为[头 (MDX)](../mdx/head-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的示例按 Internet Sales Amount 返回前 10 个日期：  
  
 `SELECT [Measures].[Internet Sales Amount] ON 0,`  
  
 `TOPCOUNT([Date].[Date].[Date].MEMBERS, 10, [Measures].[Internet Sales Amount])`  
  
 `ON 1`  
  
 `FROM [Adventure Works]`  
  
 下面的示例返回 Bike 类别包含 Geography 维度中 Geography 层次结构的 City 级别的所有成员组合的集中的前五个成员，并按照 Reseller Sales Amount 度量值进行排序（从成员集中销售额最高的成员开始）。  
  
```  
SELECT [Measures].[Reseller Sales Amount] ON 0,  
TopCount  
   ({[Geography].[Geography].[City].Members   
      *[Date].[Fiscal].[Fiscal Year].Members}  
   , 5  
   , [Measures].[Reseller Sales Amount]  
   ) ON 1  
FROM [Adventure Works]  
WHERE([Product].[Product Categories].Bikes)  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
