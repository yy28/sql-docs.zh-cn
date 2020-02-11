---
title: ：（范围）（MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 6afc3a73b958062bd6472153b2452bc0e3fa6cfc
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020617"
---
# <a name="-range-mdx"></a>:（范围）(MDX)


  执行一个集运算以返回一个自然排序集，它将两个指定成员作为端点，并将这两个指定成员之间的所有成员作为该集的成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression : Member_Expression      
```  
  
#### <a name="parameters"></a>parameters  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 包含指定成员以及指定成员之间的所有成员的集。  
  
## <a name="remarks"></a>备注  
 两个参数所指定的成员必须位于给定维度的同一级别和层次结构中。 如果这两个参数指定相同的成员，则 **：（范围）** 运算符将返回只包含指定成员的集。 如果第一个参数为 Null，则该集包含从第二个参数中指定的成员级别开始直到包括该成员的所有成员。 如果第二个参数为 Null，则该集包含从第一个参数中指定的成员开始直到包括同一级别最后一个成员的所有成员。  
  
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
 [Mdx 运算符引用 &#40;MDX&#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
