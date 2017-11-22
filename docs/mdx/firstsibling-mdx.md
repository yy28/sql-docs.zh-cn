---
title: "FirstSibling (MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: FIRSTSIBLING
dev_langs: kbMDX
helpviewer_keywords: FirstSibling function
ms.assetid: ed2fbd36-6665-4445-a894-cbeca29584ab
caps.latest.revision: "30"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: 1c1df81561dd8dc81a9cd3c302a94478e3af4794
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="firstsibling-mdx"></a>FirstSibling (MDX)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回成员的父成员的第一个子成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Member_Expression.FirstSibling   
```  
  
## <a name="arguments"></a>参数  
 *Member_Expression*  
 返回成员的有效多维表达式 (MDX)。  
  
### <a name="example"></a>示例  
 以下查询将返回 Fiscal 层次结构中 Fiscal Year 2003 的第一个同级，即 Fiscal Year 2002。  
  
```  
SELECT [Date].[Fiscal].[Fiscal Year].&[2003].FirstSibling ON 0  
FROM [Adventure Works]  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 函数引用 &#40;MDX &#41;](../mdx/mdx-function-reference-mdx.md)  
  
  
