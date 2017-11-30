---
title: "除 (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
ms.assetid: 9fe4a47b-d5e8-4dc7-ad4a-3e47ab463f03
caps.latest.revision: "5"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ec7d1cf6bf0cd7b702d633c4022230f93a686b53
ms.sourcegitcommit: 9fbe5403e902eb996bab0b1285cdade281c1cb16
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/27/2017
---
# <a name="divide-mdx"></a>除 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
