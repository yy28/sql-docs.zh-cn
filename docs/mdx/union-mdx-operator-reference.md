---
title: "+ （并集）(MDX) |Microsoft 文档"
ms.custom: 
ms.date: 03/02/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords: +
dev_langs: kbMDX
helpviewer_keywords:
- union operator (+)
- + (union operator)
ms.assetid: 6c6dfca2-7413-452a-98a2-3d8c58a8a3e6
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.openlocfilehash: fdad6eed18e3c5ef51c069c4cee4395d8d48d571
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="union---mdx-operator-reference"></a>联合的 MDX 运算符参考
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  执行一个集运算以返回两个集的并集并删除重复成员。  
  
## <a name="syntax"></a>语法  
  
```  
  
Set_Expression + Set_Expression      
```  
  
#### <a name="parameters"></a>Parameters  
 *Set_Expression*  
 返回集的有效多维表达式 (MDX)。  
  
## <a name="return-value"></a>返回值  
 一个包含两个指定集的成员的集。  
  
## <a name="remarks"></a>注释  
 **+ （联合）**运算符在功能上等效于[联合 &#40;MDX &#41;](../mdx/union-mdx.md)函数。  
  
## <a name="examples"></a>示例  
 下面的示例演示了此运算符的用法。  
  
```  
-- This member returns the gross profit margin for each year for North American countries.  
SELECT   
    [Date].[Calendar].[Calendar Year].Members ON 0,  
    {[Sales Territory].[Sales Territory].[Country].[United States]} +  
     {[Sales Territory].[Sales Territory].[Country].[Canada]} ON 1  
FROM  
    [Adventure Works]  
WHERE  
    ([Measures].[Gross Profit Margin])  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDX 运算符参考 &#40;MDX &#41;](../mdx/mdx-operator-reference-mdx.md)  
  
  
