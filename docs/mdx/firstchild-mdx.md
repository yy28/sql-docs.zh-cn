---
description: FirstChild (MDX)
title: FirstChild (MDX) |Microsoft Docs
ms.date: 06/04/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: mdx
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
ms.openlocfilehash: 60194581eb5bd2bb7f0a6252ca33062b60809706
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88387483"
---
# <a name="firstchild-mdx"></a>FirstChild (MDX)


  返回指定成员的第一个子成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.FirstChild   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
### <a name="example"></a>示例  
 下面的查询返回 Fiscal 层次结构中 2003 会计年度的第一个子级，也就是 2003 会计年度的第一个半期。  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstChild ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [LastChild &#40;MDX&#41;](../mdx/lastchild-mdx.md)   
 [MDX 函数引用 (MDX)](../mdx/mdx-function-reference-mdx.md)  
  
  
