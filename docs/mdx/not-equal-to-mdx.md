---
title: '&lt;&gt; （不等于）(MDX) |Microsoft Docs'
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ac3241e7d6acd8ba883cdd59f9410f4a0fd9187d
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63277517"
---
# <a name="ltgt-not-equal-to-mdx"></a>&lt;&gt; （不等于）(MDX)


  执行比较运算，以确定一个多维表达式 (MDX) 的值是否不等于另一个 MDX 表达式的值。  
  
## <a name="syntax"></a>语法  
  
```  
  
MDX_Expression <> MDX_Expression  
```  
  
#### <a name="parameters"></a>Parameters  
 *MDX_Expression*  
 有效的 MDX 表达式。  
  
## <a name="return-value"></a>返回值  
 布尔值，具体情形如下：  
  
-   **true**如果两个参数都非空，并且第一个参数不等于第二个参数。  
  
-   **false**如果两个参数都非空，并且第一个参数等于第二个参数。  
  
-   如果两个参数或其中任何一个参数计算出来的值为空值，则为 Null。  
  
## <a name="see-also"></a>请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
