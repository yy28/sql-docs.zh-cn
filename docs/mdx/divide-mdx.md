---
title: 除（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6184aa9d932355cd935a9131848ec27895faea5f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68049306"
---
# <a name="divide-mdx"></a>除 (MDX)


  执行除法运算，并在被0除时返回备用结果或空白（）。  
  
## <a name="syntax"></a>语法  
  
```  
  
Divide (<numerator>, <denominator> [,<alternateresult>])  
```  
  
## <a name="arguments"></a>参数  
 *numerator*  
 被除数或要相除的数字。  
  
 *denominator*  
 除数或要除以的数字。  
  
 *备用结果*  
 可有可无除数为零时返回的值导致错误。 如果未提供，则默认值为空白（）。  
  
## <a name="remarks"></a>备注  
 被 0 除时的备用结果必须是一个常量。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 函数引用 &#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
