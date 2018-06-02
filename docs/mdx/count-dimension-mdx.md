---
title: 计数 （维度） (MDX) |Microsoft 文档
ms.date: 05/30/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: fd8d61e7907a8fb05a016dabdcb65201bffdbbdc
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577639"
---
# <a name="count-dimension-mdx"></a>Count（维度）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

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
  
  
