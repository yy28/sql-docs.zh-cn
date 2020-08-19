---
description: 算术运算符
title: 算术运算符 |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 995e7ce1cb6a3c5d06db1042c00f945ec01e1be6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88494990"
---
# <a name="arithmetic-operators"></a>算术运算符


  可以在多维表达式 (MDX) 中使用算术运算符执行算术运算，包括加法、减法、乘法以及除法。  
  
 MDX 支持下表中列出的算术运算符。  
  
|操作员|描述|  
|--------------|-----------------|  
|[+（加）](../mdx/add-mdx.md)|两个数相加。|  
|[/（除）](../mdx/divide-mdx-operator-reference.md)|将一个数除以另一个数。|  
|[*（乘）](../mdx/multiply-mdx.md)|使两个数字相乘。|  
|[-（减）](../mdx/subtract-mdx.md)|两个数相减。|  
|^（幂）|以一个数为底，另一个数为幂求值。|  
  
> [!NOTE]  
>  MDX 不包括获取数字平方根的函数。 若要获取数字的平方根，请使用 ^ 运算符进行以该数字为底、以 0.5 为幂的运算。  
  
## <a name="order-of-precedence"></a>优先顺序  
 下列规则确定了 MDX 表达式中各算术运算符的优先顺序：  
  
-   如果表达式中有多个算术运算符，则 MDX 先计算乘除，后计算加减。  
  
-   如果表达式中的所有算术运算符都具有相同的优先顺序，则执行顺序为从左到右。  
  
-   括号中的表达式优先于所有其他运算。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [运算符 &#40;MDX 语法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
