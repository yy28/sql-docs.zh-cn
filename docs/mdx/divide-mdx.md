---
title: "除 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 9fe4a47b-d5e8-4dc7-ad4a-3e47ab463f03
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 6d139460bac6aa653da3d378de1c1b4c3cb80869
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="divide-mdx"></a>除 (MDX)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

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
  
## <a name="remarks"></a>注释  
 被 0 除时的备用结果必须是一个常量。  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
