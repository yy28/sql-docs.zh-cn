---
title: "算术运算符 |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- arithmetic operators
ms.assetid: 1dff3e20-fe9d-4155-bf06-27d6458188e9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: bc3adf599f92a74dd996a0ef090f6f42ab1fba0d
ms.contentlocale: zh-cn
ms.lasthandoff: 08/02/2017

---
# <a name="arithmetic-operators"></a>算术运算符
[!INCLUDE[tsql-appliesto-ss2008-all_md](../includes/tsql-appliesto-ss2008-all-md.md)]

  可以在多维表达式 (MDX) 中使用算术运算符执行算术运算，包括加法、减法、乘法以及除法。  
  
 MDX 支持下表中列出的算术运算符。  
  
|运算符|Description|  
|--------------|-----------------|  
|[+ （添加）](../mdx/add-mdx.md)|两个数相加。|  
|[/ （除）](../mdx/divide-mdx-operator-reference.md)|将一个数除以另一个数。|  
|[* （乘）](../mdx/multiply-mdx.md)|使两个数字相乘。|  
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
 [MDX 运算符参考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [运算符 &#40;MDX 语法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  

