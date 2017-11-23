---
title: "计数 （层次结构级别） (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: COUNT
dev_langs: kbMDX
helpviewer_keywords: Count function [MDX]
ms.assetid: 3de6a824-2ff3-47ac-9ceb-e3369a04f35d
caps.latest.revision: "33"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: ca18ec4161db5405055a3732007170167afc123c
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="count-hierarchy-levels-mdx"></a>Count（层次结构级别）(MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回层次结构中的级别数。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchy_Expression.Levels.Count  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
## <a name="remarks"></a>注释  
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
 [计数 &#40; 维度 &#41;&#40;MDX &#41;](../mdx/count-dimension-mdx.md)   
 [计数 &#40;元组 &#41;&#40;MDX &#41;](../mdx/count-tuple-mdx.md)   
 [计数 &#40;集 &#41;&#40;MDX &#41;](../mdx/count-set-mdx.md)   
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
