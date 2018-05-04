---
title: ': （范围) (MDX) |Microsoft 文档'
ms.custom: ''
ms.date: 03/02/2016
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- ':'
dev_langs:
- kbMDX
helpviewer_keywords:
- ': (range operator)'
- range operator (:)
ms.assetid: f9b36aca-4efd-49b4-9e4f-12914c1b24a6
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: erikre
ms.openlocfilehash: cba26f6b69ca22a1ab39fa753749d6a8b1a150df
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="-range-mdx"></a>:（范围）(MDX)
[!INCLUDE[ssas-appliesto-sqlas](../includes/ssas-appliesto-sqlas.md)]

  执行一个集运算以返回一个自然排序集，它将两个指定成员作为端点，并将这两个指定成员之间的所有成员作为该集的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>Parameters  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 包含指定成员以及指定成员之间的所有成员的集。  
  
## <a name="remarks"></a>注释  
 两个参数所指定的成员必须位于给定维度的同一级别和层次结构中。 如果这两个参数指定相同的成员， **: （范围）**运算符将返回包含指定的成员的集。 如果第一个参数为 Null，则该集包含从第二个参数中指定的成员级别开始直到包括该成员的所有成员。 如果第二个参数为 Null，则该集包含从第一个参数中指定的成员开始直到包括同一级别最后一个成员的所有成员。  
  
 在 MDX 中没有与此集运算符功能相同的函数。  
  
## <a name="examples"></a>示例  
 下面的示例演示了此运算符的用法。  
  
```  
-- This query returns the freight cost per user  
-- for products, averaged by month, for the first quarter.  
With Member [Measures].[Freight Per Customer] as  
 (  
     [Measures].[Internet Freight Cost]  
     /   
     [Measures].[Customer Count]  
)  
  
SELECT   
    {[Ship Date].[Calendar].[Month].&[2004]&[1] : [Ship Date].[Calendar].[Month].&[2004]&[3]} ON 0,  
    [Product].[Category].[Category].Members ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Freight Per Customer])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 运算符参考&#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
