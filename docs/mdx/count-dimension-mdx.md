---
title: 计数 （维度） (MDX) |Microsoft 文档
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
ms.assetid: 4b9c52f6-5bb0-401a-947c-e14134558b4a
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: 486b867456bff282801302293ec715d595924ba0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="count-dimension-mdx"></a>Count（维度）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回多维数据集中的层次结构数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Dimensions.Count   
```  
  
## <a name="remarks"></a>注释  
 返回多维数据集中的层次结构数，包括 `[Measures].[Measures]` 层次结构。  
  
## <a name="example"></a>示例  
 下面的示例返回 Adventure Works 多维数据集中的层次结构数。  
  
```  
WITH MEMBER measures.X AS  
  dimensions.count   
SELECT Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [计数&#40;元组&#41; &#40;MDX&#41;](../mdx/count-tuple-mdx.md)   
 [计数&#40;层次结构级别&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [计数 & #40;集 & #41;& #40;MDX & #41;](../mdx/count-set-mdx.md)   
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
