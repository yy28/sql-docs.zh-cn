---
description: Count（层次结构级别）(MDX)
title: " (MDX) )  (层次结构级别 |Microsoft Docs"
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: a5ebf525df144b0fd1dd81ba5b223045b2ecfd88
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461639"
---
# <a name="count-hierarchy-levels-mdx"></a>Count（层次结构级别）(MDX)


  返回层次结构中的级别数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>备注  
 返回层次结构中的级别数，包括 `[All]` 级别（如果存在）。  
  
> [!IMPORTANT]  
>  如果维度只包含一个可见的层次结构，则可以通过此维度的名称或此层次结构的名称引用此层次结构，原因是此维度的名称会解析为它唯一可见的层次结构。 例如，`Measures.Levels.Count` 是一个有效的 MDX 表达式，这是因为它会解析为 Measures 维度中唯一的层次结构。  
  
## <a name="example"></a>示例  
 下面的示例返回 Adventure Works 多维数据集中 Product Categories 用户定义层次结构中的级别数计数。  
  
```  
WITH MEMBER measures.X AS  
   [Product].[Product Categories].Levels.Count   
Select Measures.X ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#41; &#40;MDX&#41;&#40;维度计数 ](../mdx/count-dimension-mdx.md)   
 [&#41; &#40;MDX &#40;元组计数&#41;](../mdx/count-tuple-mdx.md)   
 [&#41; &#40;MDX&#41;&#40;集计数 ](../mdx/count-set-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
