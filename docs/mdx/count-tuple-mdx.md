---
title: Count （元组）（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 486c68e1947bfad67bc0288751d03c6042cd7f3e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68047276"
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
 [&#41; &#40;MDX&#41;&#40;维度计数](../mdx/count-dimension-mdx.md)   
 [&#41; &#40;MDX&#41;&#40;层次结构级别](../mdx/count-hierarchy-levels-mdx.md)   
 [&#41; &#40;MDX&#41;&#40;集计数](../mdx/count-set-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
