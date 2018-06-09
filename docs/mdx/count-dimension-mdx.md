---
title: 计数 （维度） (MDX) |Microsoft 文档
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ee8fe09f7a840d32511d3a208a4621612ee9939
ms.sourcegitcommit: 97bef3f248abce57422f15530c1685f91392b494
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34740146"
---
# <a name="count-dimension-mdx"></a>Count（维度）(MDX)


  返回多维数据集中的层次结构数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>Remarks  
 返回多维数据集中的层次结构数，包括 `[Measures].[Measures]` 层次结构。  
  
## <a name="example"></a>示例  
 下面的示例返回 Adventure Works 多维数据集中的层次结构数。  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>请参阅  
 [计数&#40;元组&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [计数&#40;层次结构级别&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [计数&#40;设置&#41; &#40;MDX&#41;](../mdx/count-set-mdx.md)   
 [MDX 函数引用&#40;MDX&#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
