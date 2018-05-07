---
title: 维度 (MDX) |Microsoft 文档
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
- Dimension
dev_langs:
- kbMDX
helpviewer_keywords:
- Dimension function
ms.assetid: 0e3ce539-1d34-45ca-8342-67796e11b730
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: cfdcc90f96b818a2b3592e4c914a5f34df33775f
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="dimension-mdx"></a>Dimension (MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  返回包含指定成员、级别或层次结构的层次结构。  
  
## <a name="syntax"></a>语法  
  
```  
  
Hierarchy syntax  
Hierarchy_Expression.Dimension  
  
Level syntax  
Level_Expression.Dimension  
  
Member syntax  
Member_Expression.Dimension  
  
```  
  
## <a name="arguments"></a>参数  
 *Hierarchy_Expression*  
 返回层次结构的有效多维表达式 (MDX)。  
  
 *Level_Expression*  
 返回级别的有效多维表达式 (MDX)。  
  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
### <a name="examples"></a>示例  
 下面的示例使用**维度**函数，结合**名称**函数，以返回指定成员的层次结构名称。  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Name  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 下例将 Dimension 函数与 Levels 和 Count 函数结合使用，以返回包含指定成员的层次结构中的级别数目。  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Levels.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
 下面的示例使用**维度**函数，结合**成员**和**计数**函数，以返回包含指定的成员的层次结构中的成员数。  
  
```  
WITH member measures.x as [Product].[Product Model Lines].[Model].&[HL Road Tire].Dimension.Members.Count  
SELECT measures.x on 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [计数&#40;层次结构级别&#41; &#40;MDX&#41;](../mdx/count-hierarchy-levels-mdx.md)   
 [计数 & #40;集 & #41;& #40;MDX & #41;](../mdx/count-set-mdx.md)   
 [级别&#40;MDX&#41;](../mdx/levels-mdx.md)   
 [成员&#40;设置&#41; &#40;MDX&#41;](../mdx/members-set-mdx.md)   
 [MDX 函数引用 & #40;MDX & #41;](../mdx/mdx-function-reference-mdx.md)  
  
  
