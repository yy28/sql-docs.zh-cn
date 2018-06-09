---
title: 除 (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 86b4d8c97996733396e3062e134b2e31d2819ec0
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34739796"
---
# <a name="divide-mdx"></a>除 (MDX)


  执行除法运算，并在被 0 除时返回备用结果或 BLANK()。  
  
## <a name="syntax"></a>语法  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>参数  
 *分子*  
 被除数，即被除的数字。  
  
 *分母*  
 要作为除数的除数或数量。  
  
 *alternateresult*  
 （可选）被零除而导致错误时返回的值。 如果没有提供，则默认值为 BLANK()。  
  
## <a name="remarks"></a>Remarks  
 被 0 除时的备用结果必须是一个常量。  
  
## <a name="see-also"></a>请参阅  
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
