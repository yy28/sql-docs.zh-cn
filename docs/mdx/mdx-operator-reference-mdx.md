---
title: MDX 运算符参考 (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- kbMDX
helpviewer_keywords:
- Multidimensional Expressions [Analysis Services], operators
- operators [MDX]
- MDX [Analysis Services], operators
ms.assetid: 1cdb8c31-a5f6-4430-b509-f81344f4622a
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: On Demand
ms.openlocfilehash: 5e80abbfc587b66c0059b2ae329e2ddfd009bf10
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="mdx-operator-reference-mdx"></a>MDX 运算符参考 (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  多维表达式 (MDX) 语言支持算术、逻辑、比较、集、字符串和一元运算符。 下表列出了所支持的运算符及其说明。  
  
## <a name="in-this-section"></a>本节内容  
  
|主题|Description|  
|-----------|-----------------|  
|[-&#40;注释 &#41;&#40;MDX &#41;](../mdx/comment-mdx-operator-reference.md)|表示用户提供的注释文本。|  
|[-&#40;除 &#41;&#40;MDX &#41;](../mdx/except-mdx-operator.md)|执行一个集运算，以返回两个集之间的不同项并删除重复成员。|  
|[-&#40;负 &#41;&#40;MDX &#41;](../mdx/negative-mdx.md)|执行一元运算，以返回数值表达式的负值。|  
|[-&#40;减去 &#41;&#40;MDX &#41;](../mdx/subtract-mdx.md)|执行一个算术运算，将一个数减去另一个数。|  
|[&#42;&#40;叉积 &#41;&#40;MDX &#41;](../mdx/crossjoin-mdx-operator-reference.md)|执行一个集运算以返回两个集的叉积。|  
|[&#42;&#40;乘 &#41;&#40;MDX &#41;](../mdx/multiply-mdx.md)|执行两个数相乘的算术运算。|  
|[&#40; 除 &#41;&#40;MDX &#41;](../mdx/divide-mdx-operator-reference.md)|执行算术运算，将一个数除以另一个数。|  
|[^ &#40;Power &#41;&#40;MDX &#41;](../mdx/power-mdx.md)|执行以一个数为底、另一个数为幂求值的算术运算。|  
|[注释 &#40;MDX &#41;](../mdx/comment-mdx.md)|表示用户提供的注释文本。|  
|[&#40;注释 &#41;&#40;MDX &#41;](../mdx/comment-mdx-double-slash.md)|表示用户提供的文本。|  
|[: &#40;范围 &#41;&#40;MDX &#41;](../mdx/range-mdx.md)|执行一个集运算以返回一个自然排序集，它将两个指定成员作为端点，并将这两个指定成员之间的所有成员作为该集的成员。|  
|[+ &#40;添加 &#41;&#40;MDX &#41;](../mdx/add-mdx.md)|执行两个数相加的算术运算。|  
|[+ &#40;正 &#41;&#40;MDX &#41;](../mdx/positive-mdx.md)|执行一元运算，以返回数值表达式的正值。|  
|[+ &#40;字符串串联 &#41;&#40;MDX &#41;](../mdx/string-concatenation-mdx.md)|执行一个字符串运算，以连接两个或更多字符串、元组或字符串和元组组合。|  
|[+ &#40;联合 &#41;&#40;MDX &#41;](../mdx/union-mdx-operator-reference.md)|执行一个集运算，返回两个集的并集并删除重复项。|  
|[&#60;&#40;小于 &#41;&#40;MDX &#41;](../mdx/less-than-mdx.md)|执行比较运算，以确定一个 MDX 表达式的值是否小于另一个 MDX 表达式的值。|  
|[&#60; = &#40;小于或等于 &#41;&#40;MDX &#41;](../mdx/less-than-or-equal-to-mdx.md)|执行比较运算，以确定一个 MDX 表达式的值是否小于或等于另一个 MDX 表达式的值。|  
|[&#60; &#62;&#40;不等于 &#41;&#40;MDX &#41;](../mdx/not-equal-to-mdx.md)|执行比较运算，以确定一个 MDX 表达式的值是否不等于另一个 MDX 表达式的值。|  
|[= &#40;等于 &#41;&#40;MDX &#41;](../mdx/equal-to-mdx.md)|执行比较运算，以确定一个 MDX 表达式的值是否等于另一个 MDX 表达式的值。|  
|[&#62;&#40;大于 &#41;&#40;MDX &#41;](../mdx/greater-than-mdx.md)|执行比较运算，以确定一个 MDX 表达式的值是否大于另一个 MDX 表达式的值。|  
|[&#62; = &#40;大于或等于 &#41;&#40;MDX &#41;](../mdx/greater-than-or-equal-to-mdx.md)|执行比较运算，以确定一个 MDX 表达式的值是否大于或等于另一个 MDX 表达式的值。|  
|[和 &#40;MDX &#41;](../mdx/and-mdx.md)|对两个数值表达式执行逻辑与运算。|  
|[是 &#40;MDX &#41;](../mdx/is-mdx.md)|对两个对象表达式执行逻辑比较。|  
|[不 &#40;MDX &#41;](../mdx/not-mdx.md)|对数值表达式执行逻辑非运算。|  
|[或者 &#40;MDX &#41;](../mdx/or-mdx.md)|对数值表达式执行逻辑或运算。|  
|[XOR &#40;MDX &#41;](../mdx/xor-mdx.md)|对两个数值表达式执行逻辑异运算。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 语言参考 &#40;MDX &#41;](../mdx/mdx-language-reference-mdx.md)  
  
  
