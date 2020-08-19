---
description: 除 (MDX)
title: 除以 (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 0999df34ff817131e890afade89fc5daad85796b
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88484010"
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
  
 *公分*  
 除数，或要除以的数字。  
  
 *alternateresult*  
 （可选）被零除而导致错误时返回的值。 如果没有提供，则默认值为 BLANK()。  
  
## <a name="remarks"></a>备注  
 被 0 除时的备用结果必须是一个常量。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
