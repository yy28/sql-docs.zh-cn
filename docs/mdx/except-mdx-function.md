---
title: Except （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: d53a88ce78eb5a1b106cefb0832ca1023f67c000
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68077252"
---
# <a name="except-mdx-function"></a>Except （MDX）函数


  计算两个集并删除第一个集中与第二个集中的元组重复的元组，也可以选择保留重复项。  
  
## <a name="syntax"></a>语法  
  
```  
  
Except(Set_Expression1, Set_Expression2 [, ALL ] )  
```  
  
## <a name="arguments"></a>参数  
 *Set_Expression1*  
 返回集的有效多维表达式 (MDX)。  
  
 *Set_Expression2*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 如果指定**ALL** ，则函数将保留在第一组中发现的重复项;在第二个集中找到的重复项仍将被删除。 成员的返回顺序与它们在第一个集中出现的顺序相同。  
  
## <a name="examples"></a>示例  
 以下示例说明了此函数的用法。  
  
```  
   //This query shows the quantity of orders for all products,  
   //with the exception of Components, which are not  
   //sold.  
SELECT   
   [Date].[Month of Year].Children  ON COLUMNS,  
   Except  
      ([Product].[Product Categories].[All].Children ,  
         {[Product].[Product Categories].[Components]}  
      ) ON ROWS  
FROM  
   [Adventure Works]  
WHERE  
   ([Measures].[Order Quantity])  
```  
  
## <a name="see-also"></a>另请参阅  
 [-&#40;除&#41; &#40;MDX&#41;](../mdx/except-mdx-operator.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
