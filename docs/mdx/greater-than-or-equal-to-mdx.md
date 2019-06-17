---
title: '&gt;= (大于或等于) (MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 14babb777aa4c5de85c0a0324621aebf91cb5367
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62653477"
---
# <a name="gt-greater-than-or-equal-to-mdx"></a>&gt;= (大于或等于) (MDX)


  执行比较运算，以确定一个多维表达式 (MDX) 的值是否大于等于另一个 MDX 表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
MDX_Expression >= MDX_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 布尔值，具体情形如下：  
  
-   **true**的第一个参数是否大于或等于第二个参数的值的值。  
  
-   **false**如果第一个参数的值小于第二个参数的值。  
  
-   **true**如果这两个参数均为 null 或一个参数为 null，则另一个参数为 0。  
  
## <a name="examples"></a>示例  
 下面的示例演示了此运算符的用法。  
  
```  
-- This query returns the gross profit margin (GPM)  
-- for Australia where the GPM is greater than or equal to 50%.  
With Member [Measures].[HighGPM] as  
  IIF(  
      [Measures].[Gross Profit Margin] >= .5,  
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
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
