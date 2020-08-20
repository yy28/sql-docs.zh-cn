---
description: Count（元组）(MDX)
title: " (MDX)  (元组) 计数 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 4212e3ed86d10035793cecd45ab071feb57e5abf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88500550"
---
# <a name="count-tuple-mdx"></a>Count（元组）(MDX)


  返回元组中的维度数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Tuple_Expression.Count  
```  
  
## <a name="arguments"></a>参数  
 *Tuple_Expression*  
 返回元组的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
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
 [&#41; &#40;MDX&#41;&#40;维度计数 ](../mdx/count-dimension-mdx.md)   
 [&#41; &#40;MDX&#41;&#40;层次结构级别 ](../mdx/count-hierarchy-levels-mdx.md)   
 [&#41; &#40;MDX&#41;&#40;集计数 ](../mdx/count-set-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
