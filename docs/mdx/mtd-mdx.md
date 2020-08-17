---
description: Mtd (MDX)
title: Mtd (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 398503bc60be44a0a5fcbcc329f3c455df967d7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88341374"
---
# <a name="mtd-mdx"></a>Mtd (MDX)


  按照时间维度中的年级别的约束，从给定成员所在的级别返回一组同级成员，从第一个同级成员开始到给定成员为止。  
  
## <a name="syntax"></a>语法  
  
```  
  
Mtd( [ Member_Expression ] )  
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果未指定成员表达式，则默认值为第一个层次结构的当前成员，该层次结构的第一个层次结构中的第一个维度*的类型为*"*月*"。  
  
 当级别所基于的属性层次结构的 Type 属性设置为*月份*时， **Mtd**函数是[PeriodsToDate](../mdx/periodstodate-mdx.md)函数的快捷函数。 也就是说，`Mtd(Member_Expression)` 等效于 `PeriodsToDate(Month_Level_Expression,Member_Expression)`。  
  
## <a name="example"></a>示例  
 下例将返回 2002 年 7 月（截止于 2002 年 7 月 20 日）Internet 销售的当月运费成本总和。  
  
```  
WITH MEMBER Measures.x AS SUM   
   (  
      MTD([Date].[Calendar].[Date].[July 20, 2002])  
     , [Measures].[Internet Freight Cost]  
     )  
SELECT Measures.x ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [Sum &#40;MDX&#41;](../mdx/sum-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
