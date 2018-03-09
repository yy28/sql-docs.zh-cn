---
title: "集运算符 |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: kbMDX
helpviewer_keywords: set operators [MDX]
ms.assetid: 83500d2e-44b3-49eb-a221-3ce5a58277a5
caps.latest.revision: "27"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 612312b3c295e2b9b3f45c4fdba9049036fd7b19
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="set-operators"></a>集运算符
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  在多维表达式 (MDX) 中，集运算符对成员或集进行运算并返回一个集。 通常用集运算符替换 MDX 表达式中的多个集函数。  
  
 MDX 支持下表中列出的集运算符。  
  
|运算符|Description|  
|--------------|-----------------|  
|[-（排除）](../mdx/except-mdx-operator.md)|返回两个集之间的不同项，并删除重复的成员。<br /><br /> 此运算符在功能上等效于[除](../mdx/except-mdx-function.md)函数。|  
|[*（叉积）](../mdx/crossjoin-mdx-operator-reference.md)|返回两个集的叉积。<br /><br /> 此运算符在功能上等效于[叉积](../mdx/crossjoin-mdx.md)函数。|  
|[:（范围）](../mdx/range-mdx.md)|返回自然排序的集，并将两个指定的成员作为终结点，这两个指定成员之间的所有成员都作为集的成员包括在其中。|  
|[+（并集）](../mdx/union-mdx-operator-reference.md)|返回两个集的并集，不包括重复的成员。<br /><br /> 此运算符在功能上等效于[联合 &#40;MDX &#41;](../mdx/union-mdx.md)函数。|  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)   
 [MDX 运算符参考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)   
 [运算符 &#40;MDX 语法 &#41;](../mdx/operators-mdx-syntax.md)  
  
  
