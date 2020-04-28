---
title: LastChild （MDX） |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 08f1f71497861ee1a946019ed547f40a0d6037ec
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "68098541"
---
# <a name="lastchild-mdx"></a>LastChild (MDX)


  返回指定成员的最后一个子成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.LastChild   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
### <a name="example"></a>示例  
 下例将返回 2001 年 9 月的值，它是 2002 会计年度第一个会计季度的最后一个子成员。  
  
```  
SELECT [Date].[Fiscal].[Fiscal Quarter].[Q1 FY 2002].LastChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [FirstChild &#40;MDX&#41;](../mdx/firstchild-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
