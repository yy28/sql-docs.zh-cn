---
title: 比较运算符 |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 31c73e25042df50fba9c1702e7834565c0284fbd
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740896"
---
# <a name="comparison-operators"></a>比较运算符


  可以对标量数据使用比较运算符。 可以在任何多维表达式 (MDX) 表达式中使用比较运算符。  
  
 若要检查的条件，你可以使用 MDX 语句和函数，如 MDX 中的比较运算符[IIf](../mdx/iif-mdx.md)函数。 但是，如果使用比较运算符检查条件，请确保在尝试基于该条件更改数据之前获得适当的权限。 任何人只要具有访问实际数据的权限并可以查询该数据，就可以在其他查询中使用比较运算符。 但这种访问权限并不意味着这些人具有或应当具有更改数据的适当权限。 另外，为了维护数据的完整性，需要限制能够查询和更改数据的人数。  
  
 比较运算符的计算结果为布尔数据类型，并根据所测试条件的输出结果返回 TRUE 或 FALSE。  
  
 MDX 支持下表中列出的比较运算符。  
  
|运算符|Description|  
|--------------|-----------------|  
|[=（等于）](../mdx/equal-to-mdx.md)|对于非空的参数，如果左边的参数等于右边的参数，则返回 TRUE；否则返回 FALSE。<br /><br /> 如果任一参数的计算结果等于空值或两个参数的计算结果都等于空值，此运算符将返回空值，除非进行了 `0=null` 比较，在这种情况下，布尔值中将包含 TRUE。|  
|[<>（不等于）](../mdx/not-equal-to-mdx.md)|对于非空的参数，如果左边的参数不等于右边的参数，则返回 TRUE；否则返回 FALSE。<br /><br /> 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该运算符返回空值。|  
|[>（大于）](../mdx/greater-than-mdx.md)|对于非空的参数，如果左边的参数值大于右边的参数，则返回 TRUE；否则返回 FALSE。<br /><br /> 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该运算符返回空值。|  
|[>=（大于或等于）](../mdx/greater-than-or-equal-to-mdx.md)|对于非空的参数，如果左边的参数值大于或等于右边的参数，则返回 TRUE；否则返回 FALSE。<br /><br /> 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该运算符返回空值。|  
|[<（小于）](../mdx/less-than-mdx.md)|对于非空的参数，如果左边的参数值小于右边的参数，则返回 TRUE；否则返回 FALSE。<br /><br /> 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该运算符返回空值。|  
|[<=（小于或等于）](../mdx/less-than-or-equal-to-mdx.md)|对于非空的参数，如果左边的参数值小于或等于右边的参数，则返回 TRUE；否则返回 FALSE。<br /><br /> 如果其中一个参数的计算结果为空值或这两个参数的计算结果均为空值，则该运算符返回空值。|  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)   
 [运算符&#40;MDX 语法&#41;](../mdx/operators-mdx-syntax.md)  
  
  
