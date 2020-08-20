---
description: '&lt;&gt; (不等于)  (MDX) '
title: '&lt;&gt; (不等于)  (MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 8c2651c7d542ac0a8707c20e8b32f4ba33ac7b54
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88471789"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; (不等于)  (MDX) 


  执行比较运算，以确定一个多维表达式 (MDX) 的值是否不等于另一个 MDX 表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>参数  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 布尔值，具体情形如下：  
  
-   如果两个参数均非空，并且第一个参数不等于第二个参数，**则为 true** 。  
  
-   如果两个参数均非空，并且第一个参数等于第二个参数，则**为 false** 。  
  
-   如果两个参数或其中任何一个参数计算出来的值为空值，则为 Null。  
  
## <a name="see-also"></a>另请参阅  
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
