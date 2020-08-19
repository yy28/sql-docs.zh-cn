---
description: '&gt; (大于)  (MDX) '
title: '&gt; (大于)  (MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 54be7523c074b2242bd740ec0b1665eb8dfb81fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429939"
---
# <a name="gt-greater-than-mdx"></a>&gt; (大于)  (MDX) 


  执行比较运算，以确定一个多维表达式 (MDX) 的值是否大于另一个 MDX 表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
MDX_Expression > MDX_Expression  
```  
  
#### <a name="parameters"></a>参数  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 布尔值，具体情形如下：  
  
-   如果两个参数均非空，并且第一个参数的值大于第二个参数的值，**则为 true** 。  
  
-   如果两个参数均非空，并且第一个参数的值等于或小于第二个参数的值，则**为 false** 。  
  
-   如果两个参数或其中任何一个参数计算出来的值为空值，则为 Null。  
  
## <a name="examples"></a>示例  
 以下示例查询演示了此运算符的用法。  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is more than 50%.  
With Member [Measures].[HighGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] > .5,  
      [Measures].[Gross Profit Margin],  
      null)  
SELECT   
NON EMPTY [Sales Territory].[Sales Territory Country].[Australia] ON 0,  
    NON EMPTY [Product].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[HighGPM])  
  
```  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
