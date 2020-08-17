---
description: Members（集）(MDX)
title: 成员 ( (MDX) ) 集 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0358f20d0aeba0e4d455fabadb6dc1e4361081e5
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341393"
---
# <a name="members-set-mdx"></a>Members（集）(MDX)


  返回某个维度、级别或层次结构中的成员集。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchy expression syntax  
Hierarchy_Expression.Members  
  
Level expression Syntax  
Level_Expression.Members  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定了层次结构表达式，则 **) 函数 (集成员 ** 将返回指定层次结构中所有成员的集，不包括计算成员。 若要获取层次结构中的所有成员的集合，请使用 [AllMembers &#40;MDX&#41;](../mdx/allmembers-mdx.md) 函数  
  
 如果指定了级别表达式，则 **) 函数 (集成员 ** 将返回指定级别中所有成员的集。  
  
> [!IMPORTANT]  
>  如果维度仅包含单个可见层次结构，由于在此情况下维度名称将解析为其唯一可见的层次结构，所以既可以通过维度名称也可以通过层次结构名称来引用该层次结构。 例如，因为 Measures.Members 解析为 Measures 维度中唯一的层次结构，所以 Measures.Members 是有效的 MDX 表达式。  
  
## <a name="examples"></a>示例  
 下例返回 Adventure Works 多维数据集中“日历年”层次结构的所有成员的集。  
  
```  
SELECT   
   [Date].[Calendar].[Calendar Year].Members ON 0  
FROM  
   [Adventure Works]  
  
```  
  
 下面的示例将返回 `[Product].[Products].[Product Line]` 级别中每个成员在 2003 年的订单数量。 **Members**函数返回一个集合，该集合表示级别中的所有成员。  
  
```  
SELECT   
   {Measures.[Order Quantity]} ON COLUMNS,  
   [Product].[Product Line].[Product Line].Members ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   {[Date].[Calendar Year].[Calendar Year].&[2003]}  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
