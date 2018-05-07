---
title: 计数 （元组） (MDX) |Microsoft 文档
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- COUNT
dev_langs:
- kbMDX
helpviewer_keywords:
- Count function [MDX]
ms.assetid: c8f4a570-54a8-4c00-ac4b-eef0ebdb353c
caps.latest.revision: 31
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 2df1e6b6c68f584b2dc2a28cda03caf766ad456b
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="count-tuple-mdx"></a>Count（元组）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回元组中的维度数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
 返回元组中的维度数。  
  
## <a name="example"></a>示例  
 下面的查询中的计算度量值返回值 2，这是在元组 `([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001])` 中提供的层次结构的数目：  
  
```  
WITH MEMBER MEASURES.COUNTTUPLE AS  
COUNT(([Measures].[Internet Sales Amount], [Date].[Calendar].[Calendar Year].&[2001]))  
SELECT MEASURES.COUNTTUPLE ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [计数&#40;维度&#41; &#40;MDX&#41;](../mdx/count-dimension-mdx.md)   
 [计数&#40;层次结构级别&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [计数 & #40;集 & #41;& #40;MDX & #41;](../mdx/count-set-mdx.md)   
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
